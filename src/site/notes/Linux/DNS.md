---
{"dg-publish":true,"permalink":"/linux/dns/"}
---

Tout d'abord il va fallori installer Bind9 :
```shell
sudo -s 
apt install bind9
```
Les fichiers de configuration de Bind9 sont dans `/etc/bind/`
Tout d’abord, vérifié si ces lignes sont dans le fichier named.conf :
```Shell
include "/etc/bind/named.conf.options";
include "/etc/bind/named.conf.local";
include "/etc/bind/named.conf.default-zones";
```
Dans le fichier de configuration de bind9 « named.conf.local », déclarer ses zones :
```Shell
zone "m2l.site" {
        type master;
        file "/etc/bind/db.m2l.site";
};
```
Dans db.example.com, on configure sa zone (l’IP du serveur DNS est 10.54.0.30 ):

```shell
;
; BIND data file for example.com
;
$TTL    604800
@       IN      SOA     m2l.site.       root.m2l.site. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
             IN      A       10.54.0.30
;
@            IN      NS      m2l.site.
             IN      A       10.54.0.30
wordpress    IN      A       10.54.0.30
```
`<wordpress permet d'avoir accès au site grâce à l'URL wordpress.m2l.site>`

Dans le fichier `<named.conf.options>` n'oubliez pas d'ajouter le "vrai" serveur DNS.
```Shell
forwarders {
		172.25.254.15;
		172.25.254.12;
        8.8.8.8;
    };
```
