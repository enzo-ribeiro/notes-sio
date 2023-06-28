---
{"dg-publish":true,"permalink":"/dev/3-premier-programme-en-c/"}
---

Pour programmer je vais utiliser un éditeur de code (plus simple pour la compréhension du code). Je commence avec le langage C car il peut s'avéré très important pour la suite de mes études.

Pour commencer on installe Visual Studio Code ou SublimText ou même NotePad++. Une fois notre éditeur de code installé on va se rendre sur le site suivant : https://winlibs.com pour installer notre compilateur on prendra la dernière version pour les 64 ou 32 bits selon le code que vous vouliez écrire, les libraires que vous vouliez utilser et surtout sur quelle machine les prograles seront utilisé. Pour ma part je choisi la version GCC 13.1.0 pour les 64 bits. Une fois les prérequis intallé on peut commencer notre premier programme.

Dans l'éditeur de code :
```C
#include <stdio.h>

int main(void)
{
	printf("Hello World !");
	return 0;
}
```

On enregiste le code, personnellement je l'appel "main.c". on se retrouve dans l'invite de commande de votre OS pour y taper les lignes suivantes:
```console
>cd D:\Chemin\du\fichier
>gcc main.c -o prog
```

Cette commande créera un ".exe" du nom "prog" pour lancer le programme on tape la commande suivante 
```console
>.\prog 
Hello World !
```

Maintenant que nous avons le résultat que nous voulions je vais vous expliquer le code :
```C
#include <stdio.h>
```

Cette ligne permet de faire une inclusion, cette inclusion est nécessaire à tout programme car elle permet au langage C de faire des "Input" ainsi que des "Output".

```C
int main(void)
```
déclare une fonction que le programme retournera avec `return 0;`.

```C
	printf("Hello World !")
```
Imprimera "Hello World !"/ 