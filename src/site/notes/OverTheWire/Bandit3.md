---
{"dg-publish":true,"permalink":"/over-the-wire/bandit3/"}
---

Pour ce 3ème niveau le dossier est caché il faut donc utiliser les commandes suivante.
```Shell
ls -a
> .  ..  .bash_logout  .bashrc  inhere  .profile
```

l'option `<-a>` sert à afficher les fichier/dossier caché.
on peut donc afficher le mot de passe.
```Shell
ls
>
```

Ici le fichier contenant le mot de passe est aussi caché on refait donc la manipulation prcédente.
```Shell
ls
> .  ..  .hidden

cat .hidden
> 2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
```

On peut se connecter au niveau 4.

