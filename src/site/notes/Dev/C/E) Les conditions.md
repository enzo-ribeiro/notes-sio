---
{"dg-publish":true,"permalink":"/dev/c/e-les-conditions/"}
---

Les conditions se déclarent avec `if`, `else if` et `else`. Elles se  déclarent avec des opérateurs différents que pour faire des opérations voici les opérateurs possible :
```C
/*
	== : égale à
	!= : différent de 
	<  : plus grand que 
	>  : plus petit que 
	
	&& : et
	|| : ou
	!  : not
*/
```

Voici des exemples de conditions :

- Avec un `if`
```C
int main(void)
{
	int age = 1;
	if(age < 18)
	{
	printf("Vous etes mineur(e)");
	}
	return 0
}
```

- En ajoutant un `else` 
```C
int main(void)
{
	int age = 1;
	if(age < 18)
	{
	printf("Vous etes mineur(e)");
	}
	else 
	{
	printf("Vous etes majeur(e)");
	}
	return 0
}
```

- En rajoutant un `else if`
```C
int main(void)
{
    int age = 0;
    if(age > 1 && age < 18)
    {
    printf("Vous etes mineur(e)");
    }
    else if(age < 1)
    {
    printf("Vous etes pas encore ne(e)");
    }
    else
    {
    printf("Vous etes majeur(e)");
    }
    return 0;
}
```

On peut utiliser autre chose que `if`, `else if` et `else`, en effet, on peut utiliser `switch` :
```C
int main(void)
{
    int age = 15;
    switch(age)
    {
        case 1:
            printf("Vous avez 1 an");
            break;
        case 18:
            printf("Vous avez 18 ans");
            break;
        default:
            printf("Break");
            break;
    }
    return 0;
}
```

Ici le `case` est égale à dire "dans le cas où `<variable>` est égale à". Le `break` fini "l'étape" donc ici `15 != 1` et `15 != 18` donc cette condition renvoie "Break". La partie `default` est obligatoire à chaque condition de type `switch`.