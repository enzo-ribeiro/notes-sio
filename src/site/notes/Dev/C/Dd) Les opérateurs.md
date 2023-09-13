---
{"dg-publish":true,"permalink":"/dev/c/dd-les-operateurs/"}
---

pour commencer les opérateurs en C sont les mêmes qu'en python c'est à dire :
- + (addition)
- - (soustraction)
- * (multiplication)
- / (division)
- % (modulo = le reste d'une division)

Ces opérateur devrons être placé dans une variable voici un exemple :
```C
int main(void)
{
	int nb1 = 4;
	int nb2 = 2;
	printf("4 + 2 est égale à %d", nb1 + nb2);
	return 0; 
}

> 4 + 2 est égale à 6
```

Cependant une opération peut également être écrite comme ci-dessous :
```C
int main(void)
{
	printf("4 + 2 est égale à %d", 4 + 2);
	return 0; 
}

> 4 + 2 est égale à 6
```

Maintenant que nous avons vu ca nous allons avoir comment réaliser des opérations avec des variables :
```C
int main(void)
{
    int niveauDuJoueur = 0;
    printf("entré le niveau du joueur : ");
    scanf("%d", &niveauDuJoueur);
    printf("Le joueur gagne de l'exp \n");
    niveauDuJoueur = niveauDuJoueur + 1;
    printf("Le joueur a atteint le niveau %d", niveauDuJoueur);
    return 0;
}

> entré le niveau du joueur : 10
Le joueur gagne de l'exp
Le joueur a atteint le niveau 11
```

Alors ici aucune erreure est présente mais le code peut être simplifié : 
```C
int main(void)
{
    int niveauDuJoueur = 0;
    printf("entré le niveau du joueur : ");
    scanf("%d", &niveauDuJoueur);
    printf("Le joueur gagne de l'exp \n");
    niveauDuJoueur += 1;
    printf("Le joueur a atteint le niveau %d", niveauDuJoueur);
    return 0;
}

> entré le niveau du joueur : 10
Le joueur gagne de l'exp
Le joueur a atteint le niveau 11
```

Ici nous avons simplifié le code nous avons transformé la ligne `<niveauDuJoueur = niveauDuJoueur + 1;>` en `<niveauDuJoueur += 1;>`

Pour ajouter 1 il est également possible de faire le code suivant `<variable++;>` cette opération rajoutera 1 à notre variable.