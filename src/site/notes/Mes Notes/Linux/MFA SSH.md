---
{"dg-publish":true,"permalink":"/mes-notes/linux/mfa-ssh/"}
---

Tout d'abord on va installer `<google authenticator>` 
```Shell
apt install libpam-google-authenticator
google-authenticator
###
# Un code QR serra généré ainsi que des clefs d'urgence et des clefs d'authentification
# Scannez le QR Code avec l'appli google authenticator
# Dite "yes" ou "no" aux questions demandé 
###
sudo nano /etc/pam.d/sshd
# Ajoutez la ligne suivante 
auth required pam_google_authenticator.so
```
Rendez-vous sur votre agent SSH (MobaXterm pour ma part) et générez une clef :
- [[Mes Notes/Linux/Génération de clef SSH\|Génération de clef SSH]]
De retour sur notre serveur ssh allez sur le fichier `<sshd_config>`
```Shell
sudo nano /etc/ssh/sshd_config
# Ajoutez les lignes suivantes 
ChallengeResponseAuthentication yes
PubkeyAuthentication yes
PasswordAuthentication no
AuthenticationMethods publickey,keyboard-interactive
```
Redémarrez le service sshd
```Shell 
sudo systemctl restart sshd
```

A partir de maintenant à la connexion on nous demandera le TOTP de l'appli google authenticator. 