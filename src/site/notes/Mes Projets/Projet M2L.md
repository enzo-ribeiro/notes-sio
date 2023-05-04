---
{"dg-publish":true,"permalink":"/mes-projets/projet-m2-l/"}
---

Pour ce projet réalisé en classe de BTS SIO SISR on devait réaliser une structure informatique typique d'une entreprise. J'avais besoin de :
- 1 Machine Virtuel (Debian 10)
- 2 Machines Physique (Windows)
- 1 Switch Cisco 2960
- 1 Routeur Cisco 2901

Je commencerai par expliquer comment configurer les équipements Cisco puis les machines physique sur windows ensuite la VM et pour terminer les ACLs.

## I. Configuration des équipements 
Tout d'abord sur le switch on créer 2 VLAN (10 et 20) ensuite on configure SSH et les ports voulu :

### A) Le Switch
#### 1) Les VLAN
```IOS
en
conf t
int fa0/2
no sh
ex
int fa0/10
no sh
ex
int fa0/24
no sh
ex
vlan 10
exit
int vlan 10
ip add 172.16.192.200 255.255.255.0
no shut
exit
vlan 20
exit
int vlan 20
ip add 10.0.0.200 255.255.255.0
no shut
exit
```
#### 2) SSH
```IOS
hostname SW-RIB
ip domain-name ssh-rib.com
enable secret netlab123
crypto key generate rsa
username sysadmin password netlab123
ip ssh version 2
line vty 0 4
login local
transport input ssh
transport output ssh
```

#### 3) Les Ports
```IOS
int f0/20
switchport mode access
switchport access vlan 20
exit
int f0/10
switchport mode access
switchport access vlan 10
int f0/24
switchport mode trunk
```

### B) Le Routeur
#### 1) Les Ports
```IOS
int g0/0
no sh
int g0/0.1
encapsulation dot1Q 10
ip add ip address 172.16.192.254 255.255.255.0
int g0/0.2
encapsulation dot1Q 20
ip add ip address 10.0.0.254 255.255.255.0
int g0/1
ip add 172.25.192.82 255.255.0.0
```

#### 2) SSH
```IOS
hostname RT-RIB
ip domain-name ssh-rib.com
enable secret netlab123
crypto key generate rsa
username sysadmin password netlab123
ip ssh version 2
line vty 0 4
login local
transport input ssh
transport output ssh
```

#### 3) Le NAT
```IOS
int g0/0.1
ip nat inside 
int g0/0.2
ip nat inside 
int g0/1
ip nat outside
ex
access-list 1 permit 172.16.192.254 255.255.255.0
access-list 2 permit 10.0.0.254 255.255.255.0
ip nat inside source list 1 interface GigabitEthernet0/1 overload
ip nat inside source list 2 interface GigabitEthernet0/1 overload
ip route 0.0.0.0 0.0.0.0 172.25.254.254
```

## II. Les Machines Physique
Pour les machines il suffit de changer la configuration IP :
- La machine qui héberge la VM aura pour configuration IP :
	- @ IP : 10.0.0.100
	- Sous réseaux : 255.255.255.0
	- Passerelle : 10.0.0.254
	- DNS : 10.0.0.10
- La machine du réseau LAN :
	- @ IP : 172.16.192.100
	- Sous réseaux : 255.255.255.0
	- Passerelle : 172.16.192.254 
	- DNS : 10.0.0.10
## III. La VM
La VM aura pour adresse IP 10.0.0.10 on y intallera un serveur GLPI puis un serveur DNS afin de facilité l'accès au site et pour finir un serveur HaProxy afin d'implémenter le protocole SSL.

### A) GLPI
#### 1) Installationapache2, php ...
```Shell
sudo -s
apt install apache2 php libapache2-mod-php mariadb-server -y
apt install php-mysqli php-mbstring php-curl php-gd php-simplexml php-intl php-ldap php-apcu php-xmlrpc php-cas php-zip php-bz2 php-imap -y
```
#### 2) Configuration de la base de donné
```Shell
mysql -u root -p
```
```SQL
create database db_glpi;  
grant all privileges on db_glpi.* to sysadmin@localhost identified by 'netlab123';  
exit
```
#### 3) Installation GLPI
```Shell
nano /etc/apache2/sites-available/000-default.conf
<Directory /var/www/html>
	Options Indexes FollowSymLinks
	AllowOverride All
	Require all granted  
</Directory>
service apache2 restart
cd /tmp  
wget https://github.com/glpi-project/glpi/releases/download/9.5.2/glpi-9.5.2.tgz
tar -xvzf glpi-9.5.2.tgz
rm /var/www/html/index.html  
cp -r glpi/* /var/www/html/
chown -R www-data /var/www/html
```



### B) DNS
```shell
sudo -s 
apt install bind9
```
Une fois cela fait on se rend dans le fichier `<named.conf.local>` pour y ajouter les lignes suivantes :
```Shell
zone "glpitestexam.com" {
        type master;
        file "/etc/bind/db.glpitestexam.com";
};
```
Ces lignes servent à déclarer le fichier de zone.
Ensuite on se rend dans le fichier `<db.glpitestexam.com>`
```Shell
;
; BIND data file for exemple.com
;
$TTL    604800
@       IN      SOA     glpitestexam.com.       root.glpitestexam.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
             IN      A       10.0.0.10
;
@            IN      NS      glpitestexam.com.
             IN      A       10.0.0.10
```
Pour finir on "va" dans le fichier `<named.conf.options>` pour y mettre les ACLs, ainsi que les forwarders :
```Shell
forwarders {
		172.25.254.15;
		172.25.254.12;
        8.8.8.8;
    };
## 
acl goodclients{
10.0.0.0/8;
172.16.0.0/16;
172.25.0.0/16;
10.0.0.0/24;
172.16.0.0/24;
};
##
recursion yes;
allow-recursion { goodclients; };
allow-query { any; };
```
### C) HaProxy
```Shell
sudo -s
apt install haproxy
nano /etc/haproxy/haproxy.cfg

frontend https-in
    bind 0.0.0.0:443 ssl crt /etc/haproxy/cert/
    mode http
    option httplog
    acl rib1 hdr(host) glpitestexam.com
    acl rib2 hdr(host) 10.0.0.10
    use_backend backend1 if rib1 or rib2

backend backend1
    mode http
    option httpchk
    option forwardfor except 127.0.0.1
    http-request add-header X-Forwarded-Proto https if { ssl_fc }
    server Debian10 10.0.0.10:80 maxconn 32
###

mkdir /etc/haproxy/cert
cd ~/
cp ~/<nom_du_fichier>.pfx /etc/haproxy/cert
cd /etc/haproxy/cert
openssl pkcs12 -in certglpi.pfx -out keyStore.pem -nodes
rm certglpi.pfx
```


## IV. Les ACLs
Pour les ACL Voici ce que je devais suivre :
- Le LAN devait avoir accèes au ssh, http/s et DNS de la DMZ et pour http/s partout sur internet .
- La DMZ devais se connecter en ssh, DNS, http/s partout sur internet

Ensuite on active les règles 
```IOS
!==LAN==
access-list 100 permit tcp 172.16.192.0 0.0.0.255 10.0.0.0 0.0.0.255 eq 2222
access-list 100 permit tcp 172.16.192.0 0.0.0.255 any eq www
access-list 100 permit tcp 172.16.192.0 0.0.0.255 any eq 443
access-list 100 permit tcp 172.16.192.0 0.0.0.255 10.0.0.0 0.0.0.255 eq 53
access-list 100 permit udp 172.16.192.0 0.0.0.255 10.0.0.0 0.0.0.255 eq 53

!==DMZ==
access-list 101 permit tcp 10.0.0.0 0.0.0.255 172.16.192.0 0.0.0.255 eq 22
access-list 101 permit tcp 10.0.0.0 0.0.0.255 eq 22 172.16.192.0 0.0.0.255
access-list 101 permit tcp 10.0.0.0 0.0.0.255 172.16.192.0 0.0.0.255 eq 2222
access-list 101 permit tcp 10.0.0.0 0.0.0.255 eq 2222 172.16.192.0 0.0.0.255
access-list 101 permit tcp 10.0.0.0 0.0.0.255 any eq www
access-list 101 permit tcp 10.0.0.0 0.0.0.255 any eq 443
access-list 101 permit tcp 10.0.0.0 0.0.0.255 172.16.192.0 0.0.0.255 eq 53
access-list 101 permit udp 10.0.0.0 0.0.0.255 172.16.192.0 0.0.0.255 eq 53
access-list 101 permit tcp 10.0.0.0 0.0.0.255 eq 53 172.16.192.0 0.0.0.255
access-list 101 permit udp 10.0.0.0 0.0.0.255 eq 53 172.16.192.0 0.0.0.255

!==INT==
access-list 102 permit tcp any eq 53 any
access-list 102 permit udp any eq 53 any
access-list 102 permit tcp any any eq 53
access-list 102 permit udp any any eq 53
access-list 102 permit tcp any any eq www
access-list 102 permit tcp any eq www any
access-list 102 permit tcp any any eq 443
access-list 102 permit tcp any eq 443 any

int g0/0.1
ip access-group 100 out

int g0/0.2
ip access-group 101 out

int g0/1
ip access-group 102 out
```



Et voilà notre infrastructure systèmes et réseau est en marche.