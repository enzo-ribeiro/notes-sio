---
{"dg-publish":true,"permalink":"/dev/c/b-afficher-les-variables/"}
---

Pour afficher les variables les plus utilsées voici un tableau :
| Commande | Desciption                  |
| -------- | --------------------------- |
| %d       | Nombre entier (int)         |
| %f       | Nombre à virgule (float)    |
| %c       | caractère (char)            |
| %s       | Chaîne de caractère (texte) |

Exemples :
```C 
int main(void)
{
    int entier = 45;
    printf("L'entier est %d.", entier);
    return 0;
}

> L'entier est 45.
```

Pour un nombre floattant (float) prenons l'exemple d'un prix :
```C 
int main(void)
{
    float prix = 125.99;
    printf("Le prix est %F euros.", prix);
    return 0;
}

> Le prix est 125.990000 euros.
```
Ici le prix est affiché avec 6 chiffres après la virgule alors que nous voulons que 2 chiffres après la virgule nous allons donc déclarer "%.2f" :
```C 
int main(void)
{
    float prix = 125.99;
    printf("Le prix est %.2f euros.", prix);
    return 0;
}

> Le prix est 125.99 euros.
```
