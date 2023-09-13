---
{"dg-publish":true,"permalink":"/over-the-wire/bandit4/"}
---

Ici ca se complique un peu.
```Shell
ls 
> inhere

cd inhere
ls 
> -file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09

## Il faut tester tout les fichiers pour ma part c'est le -file07
cat < -file07
> lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
```

Et voilà on a notre mot de passe. 
on peut se connecter à la 5ème machine.