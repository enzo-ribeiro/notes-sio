---
{"dg-publish":true,"permalink":"/cisco/routeur/routage-on-a-stick-ou-routage-inter-vlan/"}
---

Pour ce TP nous aurons besoins de lien trunk. 

Pour commencer on va se rendre sur la note du lien trunk :
- [[Cisco/Switch/Comment faire un lien trunk\|Comment faire un lien trunk]]

Une fois le lien trunk réalisé on va pouvoir ajouter un routeur : 
![La maquette au complet](2.PNG)

Une fois rajouté on active le port côté router :
```IOS
Routeur> en
Routeur# conf t
Routeur(config)# int Gi0/0
Routeur(config-if)# no shut
Routeur(config-if)# ex
```

Une fois cela fait on commence la R configuration du router : 
```IOS
Routeur(config)# int gi0/0.1
Routeur(config-subif)# encapsulation dot1Q 10
Routeur(config-subif)# ip address 172.16.254.254 255.255.0.0
Routeur(config-subif)# ex
Routeur(config)# int gi0/0.2
Routeur(config-subif)# encapsulation dot1Q 20
Routeur(config-subif)# ip address 172.25.254.254 255.255.0.0
```
![Ping résolu](Image/3.PNG)