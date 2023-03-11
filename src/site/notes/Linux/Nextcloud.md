---
{"dg-publish":true,"permalink":"/linux/nextcloud/"}
---

Tout d'abord mettre sa machine à jour.
```Shell
sudo -s
apt update
```
Une fois cela fait on va pouvoir commencer l'installation de apache et de quelques paquets important pour la suite .
```Shell
apt install apache2 libapache2-mod-php php php-cli php-{curl,gd,intl,memcache,xml,zip,mbstring,json} bzip2 wget
```
Maintenant on peut installer le .tar de `<nextcloud>` puis le dézippé dans le dossier ``</var/www/html/>``.
```Shell
wget https://download.nextcloud.com/server/releases/nextcloud-18.0.0.tar.bz2
tar -xjf nextcloud-18.0.0.tar.bz2 -C /var/www/html/
```
Le chemin de dossier ressemblera à ``</var/www/html/nextcloud>`` ce qui sera contraignant par la suite car quand nous voudrons accéder à notre cloud il faudra taper `<@_IP/nexcloud>` donc pour éviter ça je vous propose de réaliser la commande suivante.
```Shell
cd /var/www/html
mv nextcloud/* /var/www/html/
rm -rf nextcloud
```
Ensuite il est important de donner les droits au dossier `</var/www/html>`.
```Shell
chown -R www-data:www-data /var/www/html/
```
A partir de maintenant le nextcloud sera joignable mais il va demander un login de connexion il faudra donc une base de donné avec utilisateur et droits d'utilisation de la BDD. On utilisera MariaDB.
```Shell
apt install mariadb-server
mysql -u root -p 
CREATE DATABASE clouddb;
MariaDB [(none)]>CREATE DATABASE clouddb;
MariaDB [(none)]>GRANT ALL ON clouddb.* TO 'clouddbuser'@'localhost' IDENTIFIED BY 'password';
MariaDB [(none)]>FLUSH PRIVILEGES;
```
Maintenant vous avez un cloud totalement fonctionnel à la maison.