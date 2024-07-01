---
{"dg-publish":true,"permalink":"/grub/securiser-grub/"}
---

Pour sécuriser GRUB nous allons mettre un mot de passe avant même que GRUB se lance.

Nous allons générer d'un MDP chiffré : 
```Shell
sudo grub-mkpassw-pbkdf2 | sudo tee -a /etc/grub.d/40_custom
```
Après cette commande la création d'un mot de passe vous sera demandé, ce sera le mot de passe de sécutisation.

Il faudra installer la configuration :
```Shell
grub-mkconfig -o /boot/grub/grub.cfg
```

Attention cette configuration nécessite un reboot du système. 
Au reboot le système sera en QWERTY !!