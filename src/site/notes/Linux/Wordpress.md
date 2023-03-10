---
{"dg-publish":true,"permalink":"/linux/wordpress/"}
---

Requirements :
-   Serveur web : Nginx ou Apache avec le module mod-rewrite
-   Espace disque : Au moins 1 Go
-   PHP : Version 7.4 ou supérieure
-   Base de données : MySQL 5.015 ou supérieur
-   RAM (Random Access Memory) : Au moins 512 Mo
-   CPU (Central Processing Unit) : Au moins 1,0 GHz
-   Prise en charge de HTTPS

Pour commencer on va installer Apache2 :
```Shell
sudo -s
apt install apache2 -y 
```

Une fois installer il faut vérifier si apache fonctionne 
```Shell
systemctl status apache
ip a 
http://<@_IP_obtenu>(dans le navigateur)
```
Vous devriez avoir une page avec le titre "Apache2 Debian Default Page". Si la page apparait c'est que apache est bien installé.

Ensuite on va installer php et ses paquets utile et nécessaire.
```Shell
apt install php php-pdo php-mysql php-zip php-gd php-mbstring php-curl php-xml php-pear php-bcmath -y 
```
Une fois installé on vérifie que php ce soit bien installé
```Shell
php -v
```
Maintenant on va s'assurer que le moteur de script soit bien fonctionnel 
```Shell
cd /var/www/html
nano index.php
	<php
	phpinfo();
	?>
http://<@_IP_obtenu>/phpinfo.php(dans le navigateur)
```

Une fois apache2 et php installé on aura besoin d'une base de donnée pour ici on installera mariadb
```Shell
apt install mariadb-server -y
```
Ensuite on vérifie que mariadb est bien installé
```Shell
mariadb -v
```
Maintenant on ragrde les tables créer de base
```Shell
mariadb -u root -p
```
```SQL
MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
+--------------------+
1 rows in set (0,001 sec)
```
On créer notre base de donnée
```SQL
MariaDB [(none)]> CREATE DATABASE WP_ID001;
# (Répose de la commande)Query OK, 1 row affected (0.001 sec)
MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| WP_ID001           |
| information_schema |
+--------------------+
2 rows in set (0,001 sec)
```
Ici nous allons créer notre User et lui donner les droits
```SQL
CREATE USER 'sysadmin'@'localhost' IDENTIFIED BY 'netlab123';
GRANT ALL PRIVILEGES ON WP_ID011.* TO sysadmin@localhost;
FLUSH PRIVILEGES;
exit
```
Notre table est créée on peut passer à l'installation de Wordpress
```Shell
cd /tmp
wget https://wordpress.org/latest.zip
cd /var/www/html
rm index.html
```
Maintenant on va unzip le `<latest.zip>` 
```Shell
apt install zip
unzip /tmp/latest.zip -d /var/www/html
```
Une fois fait on doit donner les droits au dossier
```Shell
chown -R www-data:www-data /var/www/html/wordpress
```
Voila il ne manque plus qu'a suivre les étapes proposé par wordpress.