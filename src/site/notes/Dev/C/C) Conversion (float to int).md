---
{"dg-publish":true,"permalink":"/dev/c/c-conversion-float-to-int/"}
---

Pour faire une conversion d'un float à un int il faut les lignes suivantes:
```C
int main(void)
{
    float nombre = 125.99;
    int entier = (int)nombre;
    printf("L'entier du nombre est %d", entier);
    return 0;
}

> L'entier du nombre est 125
```