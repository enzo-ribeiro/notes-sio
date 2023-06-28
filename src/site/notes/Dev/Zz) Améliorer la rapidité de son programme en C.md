---
{"dg-publish":true,"permalink":"/dev/zz-ameliorer-la-rapidite-de-son-programme-en-c/"}
---

Pour calculer plus rapidement on peut utiliser "register" qui va faire fonctionner la mémoire du CPU qui est plus petite donc plus rapide à calculer.
```C 
int main(void)
{
	register int nombre = 5;
	printf("Le nombre est %d", nombre)
}

> Le nombre est 5
```

A contrario on peut déclarer que nous ne voulons pas qu'une variable soit enregistré dans la mémoire du CPU pour éviter de la surcharger, on utilisera alors "volatile".
```C 
int main(void)
{
	volatile int nombre = 5;
	printf("Le nombre est %d", nombre)
}

> Le nombre est 5
```

Les compilateurs de nos jours le font tout seul donc il n'est pas nécessaire de le mettre dans nos programmes sauf si vous utilisez des anciens compilateur ou le bloc note comme éditeur de code.