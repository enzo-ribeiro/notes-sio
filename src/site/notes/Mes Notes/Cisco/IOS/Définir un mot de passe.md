---
{"dg-publish":true,"permalink":"/mes-notes/cisco/ios/definir-un-mot-de-passe/"}
---

Pour définir un mot de passe sur un Switch ou un routeur c'est la même procédure. Nous nous rendons donc sur le Switch désiré.
```IOS
Switch>en
Switch#conf t
Switch(config)#enable password cisco
```
Maintenant chaque fois que vous voulez entrez en mode configuration globale il vous faudra un mot de passe. Un petit détail me chagrine le mot de passe apparaît en clair : 
```IOS
hostname Switch
!
enable password cisco
!
!
```
Pour sécuriser ça on va enlever le `<password>` et metter `<secret>` à la place 
```IOS
Switch>en
Switch#conf t
Switch(config)#enable secret cisco
```
Et à partir de maintenant on a un mot de passe sécurisé :
```IOS
hostname Switch
!
enable password enable secret 5 $1$mERr$hx5rVt7rPNoS4wqbXKX7m0
!
!
```

Il est également possible de mettre un mot de passe dès l'arriver sur le switch:
```IOS
Switch>en
password :
Switch#conf t
Switch(config)#line console 0
Switch(config-line)#password class
Switch(config-line)#login
```


