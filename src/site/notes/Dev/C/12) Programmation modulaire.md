---
{"dg-publish":true,"permalink":"/dev/c/12-programmation-modulaire/"}
---

La programmation modulaire est le fait de programmer avec plusieurs fichiers.
Ici nous allons programmer avec un fichier `<main.c>`, `<player.c>` et `<player.h>`. 
Les noms changerons selon vous.

main.c :
```C
#include <stdio.h>
#include "player.h"

int main(void)
{
    bonjour();
    return 0;
}
```
Dans ce fichier nous déclarons l'inclusion de fichier `<player.h>` avec des guillemets et nom sous forme de balisage.

player.c :
```C 
#include <stdio.h>
#include "player.h"

void bonjour(void)
{
    printf("Bonjour :)\n");
}
```
Ici on fais de même pour l'inclusion. Ce fichier comportera le code la fonction `<bonjour>`.

player.h :
```C
#ifndef __TOTO__
#define __TOTO__

void bonjour(void);

#endif
```
Les lignes 1,2 et 6 permet d'inclure conrectement les bibliothèques. Il est important de mettre ces lignes à chaque bibliothèque que vous allez créer. Le nom n'importe en rien ici on aurait put les nommés `<__TATA__>`, `<__TRUC__>`, `<__CHOSE__>`  peut importe.