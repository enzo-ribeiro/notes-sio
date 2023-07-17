---
{"dg-publish":true,"permalink":"/dev/c/13-define/"}
---

`<#define>` a plusieurs fonction :
- Créer une constante
```C
#define PI = 3.14

int main(void)
{
    printf("PI est égale à %d", PI);
    return 0;
}
```

- Pouvoir "remplacer" des commandes
```C
#include <stdio.h>
#define afficher printf

int main(void)
{
    afficher("coucou");
    return 0;
}
```