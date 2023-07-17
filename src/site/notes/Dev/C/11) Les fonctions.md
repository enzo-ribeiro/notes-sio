---
{"dg-publish":true,"permalink":"/dev/c/11-les-fonctions/"}
---

Les fonctions servent à éviter la répétition de code pour changer qu'une valeur et pas plusieurs à chaque fois qu'on doit changer un truc.

```C
int init_ball(int posX)
/*      
	Ici on à le nom de la fonction (on l'appellera plus tard)
	Nous avons le type de variable ic c'est un entier avec le int
	Ensuite nous avons le nom de la variable qui sera retourné
*/
{
	posX = 150;
	return posX;
}

int main(void)
{
	int BalleX;
	BalleX = init_ball(BalleX);
	printf("La fonction est égale à : %d\n", BalleX);
	return 0;
}

> La fonction est égale á : 150
```

Admettons que nous changeaons la valeur de posX, le résultat sera le suivant :
```C
int init_ball(int posX)
{
	posX = 1;
	return posX;
}

int main(void)
{
	int BalleX;
	BalleX = init_ball(BalleX);
	printf("La fonction est égale à : %d\n", BalleX);
	return 0;
}

> La fonction est égale á : 1
```