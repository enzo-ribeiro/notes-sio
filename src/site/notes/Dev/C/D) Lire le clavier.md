---
{"dg-publish":true,"permalink":"/dev/c/d-lire-le-clavier/"}
---

Pour lire le clavier nous avons plusieurs façon, ici nous verrobs avec le plus simple mais le moins sécurisé : "scanf":
```C
int main(void)
{
    int ageUser = 0;
    printf("Quel age avez-vous ? ");
    scanf("%d", &ageUser);
    /*
    Les variables sont stocké dans une adresse hexadécimal
    soit par exemple OxFA95D7. Donc :
    ageUser  = Variable
    &ageUser = Adresse de variable
    */
    printf("Vous avez %d ans. \n", ageUser);
    return 0;
}

> Quel age avez-vous ? 19
Vous avez 19 ans.
```