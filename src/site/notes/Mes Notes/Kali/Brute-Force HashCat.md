---
{"dg-publish":true,"permalink":"/mes-notes/kali/brute-force-hash-cat/"}
---

Tout d'abord, HashCat est un outil puissant et flexible pour le craquage de mots de passe, essentiel pour les tests de pénétration et les évaluations de sécurité.

Voici quelques exemple d'utilisation de HashCat : 

BruteForce : 
``` Shell
hashcat -a 3 -m 22000 hashes.txt ?u?d?d?u?d?u?d?d
```
	-a 3 : applique le mode bruteforce.
	-m 22000 : précise un mode spécifique. Ici le WPA. il existe un grand nombre de mode hashcat -h pour tous les connaître.
	 hashes.txt : fichier qui comporte le hash.
	 Ensuite nous précisons les paramètres du bruteforce
		 ?u : lettre majuscule
		 ?d : decimal
		 ?l : lettre minuscule
		 ?s : caractère spéciaux

Wordlist :
``` Shell
hashcat -m 22000 hashes.txt /usr/share/wordlists/rockyou.txt
```
	 -m 22000 : précise un mode spécifique. Ici le WPA. il existe un grand nombre de mode hashcat -h pour tous les connaître.
	 hashes.txt : fichier qui comporte le hash.
	 /usr/share/wordlists/rockyou.txt précisions de la wordlists que nous voulons utiliser.

Voici des exemples d'utilisation de Hashcat.