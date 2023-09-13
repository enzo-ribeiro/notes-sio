---
{"dg-publish":true,"permalink":"/dev/c/cc-avoir-une-constante/"}
---

Il se peu que dans un programme on ai besoin de déclarer une variable invariable comme le nombre PI par exemple on sait que PI est égale à 3.14 et cela ne change jamais. Donc pour éviter qu'un developpeur ne change cette variable on doit la déclarer comme constante :

```C
int main(void)
{
    const float PI = 3.14;
    float PI = 5.13;
    printf("PI est égale à %d", PI);
    return 0;
}

> main.c: In function 'main':
main.c:6:11: error: conflicting type qualifiers for 'PI'
    6 |     float PI = 5.13;
      |           ^~
main.c:5:17: note: previous definition of 'PI' with type 'float'
    5 |     const float PI = 3.14;
      |                 ^~
```
Si un developpeur voudra changer la ligne au moment de la compilation il aura le message d'erreur précédent, car PI ne pas être changé grâce à la déclaration de la constante.

Ou sinon :
```C
#include <stdio.h>
#define PI = 3.14

int main(void)
{
    printf("PI est égale à %d", PI);
    return 0;
}
```