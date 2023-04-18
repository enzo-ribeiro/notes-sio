---
{"dg-publish":true,"permalink":"/securite/honey-pot/"}
---

Le HoneyPot fonctionnera sur une machine virtuelle sous Ubuntu.
Tout d'abord on installera git et opencanary (notre honeypot)
```Shell
sudo -s
apt install python3-dev python3-pip python3-virtualenv python3-venv python3-scapy libssl-dev libpcap-dev git -y 
git clone https://github.com/thinkst/opencanary.git
```
Ensuite on créer notre environnement virtuel puis on l'active
```Shell
virtualenv env/
. env/bin/activate
opencanaryd --copyconfig
```
Maintenant on va configurer notre fichier de conf
```Shell
nano /etc/opencanaryd/opencanary.conf
*Ici changer la ligne qui correspond à ce que vous voulez ici on veut le port 80 pour le web et on va donc changez la ligne suivante*
"http.enabled": false, --> "http.enabled": true, 
```
On démarre le service avec la commande suivante 
```Shell
opencanaryd --start
```
on se rend sur le "site" qui est notre honeypot avec l'adresse IP de notre ubuntu sur un navigateur (précisez le port si vous l'avez chnagez). Une page de log de DiskStation apparaît, c'est notre piège.
L'attaquant va essayer de se connecter et nous allons récupérer son IP ainsi que les identifiants qu'il a essayé de rentrer. Pour vérifier cela on va se rendre sur notre machine hébergeant le honeypot et taper la comande suivante 
```Shell
tail /var/tmp/opencanary.log
```
Elle nous returnera les lignes suivantes 
```Shell

{"dst_host": "192.168.1.67", "dst_port": 80, "local_time": "2023-04-18 20:41:07.745543", "local_time_adjusted": "2023-04-18 22:41:07.745562", "logdata": {"HOSTNAME": "192.168.1.67", "PASSWORD": "netlab123", "PATH": "/index.html", "SKIN": "nasLogin", "USERAGENT": "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/112.0", "USERNAME": "sysadmin"}, "logtype": 3001, "node_id": "opencanary-1", "src_host": "192.168.1.214", "src_port": 52671, "utc_time": "2023-04-18 20:41:07.745559"}
```
Ici on a le l'adresse IP de l'attaquant "192.168.1.214", les identifiants de connexion "USERNAME": "sysadmin" "PASSWORD": "netlab123" et le navigateur utilisé par ce dernier "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/112.0".