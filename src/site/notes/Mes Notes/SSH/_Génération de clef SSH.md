---
{"dg-publish":true,"permalink":"/mes-notes/ssh/generation-de-clef-ssh/"}
---

Tout d'abord i lfaut se retrouver sur la machine en question 
```Shell
ssh-keygen -t rsa
```
une fois cette commande entrée il faut repondre aux questions suivante 
```Shell
Enter file in which to save the key (/root/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

Maintenant que cela est fait on peut envoyer cette clef 
```Shell
ssh-copy-id 'username'@'@_ip'
```