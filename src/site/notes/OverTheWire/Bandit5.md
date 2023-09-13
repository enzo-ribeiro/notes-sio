---
{"dg-publish":true,"permalink":"/over-the-wire/bandit5/"}
---

Ce niveau est particuler car c'est une commande que nous âs encore utilisé.
```Shell
ls
> inhere

cd inhere
ls
> maybehere00  maybehere02  maybehere04  maybehere06  maybehere08  maybehere10  maybehere12  maybehere14  maybehere16  maybehere18
maybehere01  maybehere03  maybehere05  maybehere07  maybehere09  maybehere11  maybehere13  maybehere15  maybehere17  maybehere19

## arrivé ici il faut mettre les condition déclaré dans la consigne 
find ./ -type f -size 1033c ! -executable
## ./ -type f déclare que nous voulons un fichier avec des characters et rien d'autre.
## -size 1033c déclare que nous cherchons un fichier de 1033 byte.
## ! -executable déclare que nous ne voulons pas d'executable.
> ./maybehere07/.file2

cat < maybehere07/.file2 
> P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
```