---
{"dg-publish":true,"permalink":"/grub/grub-c-est-quoi/"}
---

GRUB est un programme d'amorçage de micro-ordinateur. Il s'exécute à l'allumage de l'ordinateur.
Il est possible de coutouner les restrictions de mot de passe en faisant une manipulation au démarrage de GRUB.
Voici un exemple de coutournement de mot de passe sur GRUB.

Au démarrage de GRUB choisissez le système voulu (Pour moi c'est Debian) et tapez `<e>`.
Une fenêtre s'affiche `<GNU GRUB version (version de votre GRUB)>`.
Cherchez la ligne où il y a une ligne qui contient "ro quiet" à la suite de cette ligne rajuotez `<init=/bin/bash>`.
Après avoir rajoutez cette commande faitesle raccourcis `<ctrl + x>`

Une fois dans la console il faut déclarer que nous voulons démarrer en mode lecture-écriture (rw) lecture-seule (ro)
```Shell
mount -n -o remount,rw /
## Ensuite il suffit de reset le mot de passe

passwd
## Choisissez votre mot de passe
```

Une fois cela fait redémarrez le système avec `<ctrl + alt + del>` au redémarrage le mot de passe aura été changé.