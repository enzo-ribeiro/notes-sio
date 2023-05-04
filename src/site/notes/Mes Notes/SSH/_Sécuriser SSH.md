---
{"dg-publish":true,"permalink":"/mes-notes/ssh/securiser-ssh/"}
---


Tout d'abors il faut se retrouver sur le serveur SSH ici l'adresse est `<10.54.0.10>` et notre service permettant la connexion SSH ici `<MobaXterm>`.
```MobaXterm
ssh sysadmin@10.54.0.10
Warning: Permanently added '10.54.0.10' (ECDSA) to the list of known hosts.
sysadmin@10.54.0.10's password:
Linux Wordpress 4.19.0-23-amd64 #1 SMP Debian 4.19.269-1 (2022-12-20) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
You have new mail.
Last login: Thu Mar  9 09:35:00 2023
Initialising new SSH agent...
sysadmin@Wordpress ~$ 
```
Si SSH n'est pas installer rendez-vous physiquement sur la machine et tapez les commandes suivantes.
```Shell
sudo -s
apt install openssh-server
```
# I. Changement de Port

Maintenant que SSH est installé on peut commencer à le sécuriser.
```Shell
nano /etc/ssh/sshd_config
# Changez le port de connexion mettez 2222 ou 4592 ou 9351 bref comme vous voulez cela fera perdre du temps aux personnes mal intentionné. Puis décommenté la ligne.
Port 2222
```
Redémmarrez le serveur.
Maintenant pour se connecter en SSH il faudra donc maintenant préciser le port donc pour nous ca donnera ca 
```Shell
ssh sysadmin@10.54.0.10 -p 2222
Warning: Permanently added '10.54.0.10' (ECDSA) to the list of known hosts.
sysadmin@10.54.0.10 s password:
Linux Wordpress 4.19.0-23-amd64 #1 SMP Debian 4.19.269-1 (2022-12-20) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
You have new mail.
Last login: Thu Mar  9 09:35:00 2023
Initialising new SSH agent...
sysadmin@Wordpress ~$ 
```

# II. Timeout SSH
Ensuite nous pouvons configurer un timeout sur les connexion SSH afin de déconnecter le SSH au bout d'un certain moment d'innactivité .(Toujoours dans le même fichier on va configurer cela)
```Shell 
ClientAliveInterval 600
ClientAliveCountMax 0
```
-   **ClientAliveInterval** - indique le délai d'attente en secondes. Après x secondes, le serveur SSH enverra un message au client demandant une réponse.

-   **ClientAliveCountMax** - indique le nombre total de messages de vérification envoyés par le serveur SSH sans obtenir de réponse du client SSH.
Redémmarrez le serveur.

# III. No login root
Empêcher le user root de se connecter en SSH.
Toujours dans le même fichier on va modifier la ligne suivante.
```Shell 
PermitRootLogin No
```
Redémmarrez le serveur.

# IV. Authentification par clef
Ici on se rend sur MobaXterm et on génère la paire de clef
```Shell
ssh-keygen -b 4096
Generating public/private rsa key pair.
Enter file in which to save the key (/home/mobaxterm/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in id_rsa.
Your public key has been saved in id_rsa.pub.
The key fingerprint is:
SHA256:0I0jp5rlxYD5K3CSfLQFAIIF/GyoW2cuYhbI6s8LEkI ribeiro@N110-05
The key s randomart image is:
+---[RSA 4096]----+
|*+o..            |
|o.   + . o       |
| E+ + = = .      |
|.o * + B .       |
|* * + + S        |
|++.=o= o         |
|o+.++ o          |
|=o+ ..           |
|+o.=.            |
+----[SHA256]-----+
```
Maintenant il suffit de déclarer public dans le repertoire `<~/.ssh/authorized-keys>`. Enzuite il faudra déclarer la clef privée dans MobaXTerm à la création de la session SSH. et voilà le tour est joué.