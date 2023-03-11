---
{"dg-publish":true,"permalink":"/cisco/routeur/ssh-avec-un-routeur-cisco/"}
---

Réalisé sur un Routeur. Pour un switch veuillez suivre la fiche ci-dessous:
- [[Cisco/VLAN/Donner une IP à un VLAN\|Donner une IP à un VLAN]]
Pour commencer on va donner un nom à notre Routeur.
```IOS
Router(config)# hostname RT-RIB
RT-RIB(config)# ip domain-name rt-rib.com
```
Maintenant on va sécuriser le mode privilégié du routeur.
```IOS
RT-RIB(config)# enable secret <mot_de_passe>
```
Ensuite, nous devons générer une paire de clés asymétrique. Il faut aussi chiffrer ces clés, on utilisera le protocole RSA:
```IOS
RT-RIB(config)# crypto key generate rsa
The name for the keys will be: rt-rib.com
Choose the size of the key modulus in the range of 360 to 2048 for your
General Purpose Keys. Choosing a key modulus greater than 512 may take a few minutes.

How many bits in the modulus [512]: 1024
% Generating 1024 bit RSA keys, keys will be non-exportable. . . [OK]

RT-RIB(config)# 
```
Après ça il faut créer un utilisateur avec `<usename:password>`.
```IOS
RT-RIB(config)# username sysadmin password netlab123
```

Une fois cela fait on doit activer le protocole SSH.
```IOS
RT-RIB(config)# ip ssh version 2
```

### Petite parenthèse sur les commandes qui vont suivre

Pour se connecter sur appareil à distance, il y a deux protocoles principaux: `Telnet` et `SSH`. Telnet est un protocole simple qui fonctionne bien, mais qui n’est pas du tout sécurisé et crypté: c’est à dire que n’importe qui peut intercepter les trames de communication entre vous et l’appareil.

SSH est quand lui crypté (grâce aux clés que nous avons généré plus tôt). La norme veut donc que l’on force notre switch à ne communiquer qu’en SSH, et que la connexion en Telnet soit impossible (pour plus de sécurité).

C’est ce que l’on va faire maintenant.

On va d’abord forcer notre switch à n’accepter que la communication entrante en SSH:

```IOS
RT-RIB(config)# line vty 0 4
RT-RIB(config)# login local
RT-RIB(config-line)# transport input ssh
```

Puis on fait de même pour la communication sortante:

```IOS
RT-RIB(config-line)# transport output ssh
```