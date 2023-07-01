---
{"dg-publish":true,"permalink":"/dev/10-les-boucles-en-c/"}
---

Il y a 3 types de boucles `while`, `do` et `for`. Voici comment les utilisées:
- While :
```C
int main(void)
{
    int i = 0;
    while (i < 3)
    {
        printf("Aya !!\n");
        i++;
    }
    return 0;
}

>Aya !!
Aya !!
Aya !!
```
`i` est un compteur dans le quel on incrémente +1 à chaque fois que la boucle fait un tour. Ici j'ai décidé de faire une boucle à trois tours.

- Do :
```C
int main(void)
{
    int i = 0;
    do
    {
        printf("Aya !!\n");
        i++;
    }
    while (i < 5);
    return 0;
}

>Aya !!
Aya !!
Aya !!
Aya !!
Aya !!
```
La boucle `do` exécutera toujours au moins une fois le programme car la condition est vérifié juste après.

- For 
```C
int main(void)
{
    int i = 0;
    for (i = 0; i < 10; i++)
    {
        printf("Aya !\n");
    }
    return 0;
}

>Aya !!
Aya !!
Aya !!
Aya !!
Aya !!
Aya !!
Aya !!
Aya !!
Aya !!
Aya !!
```
La boucle `for` est plus compact en effet le compteur et l'incrémentation se font à la déclaration de la boucle et non dans cette déclaration.