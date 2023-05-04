---
{"dg-publish":true,"permalink":"/mes-notes/cisco/vlan/donner-une-ip-a-un-vlan/"}
---

```IOS
Switch>en
Switch#conf t
Switch(config)#int vlan <n°VLAN>
Switch(config-if)#ip add 192.168.1.250 255.255.255.0(Masque sous réseau)
Switch(config-if)#no shut
```
Voilà maintenant votre VLAN à une adresse IP. Pratique pour une connexion SSH disponible ci-dessous :
- [[Mes Notes/Cisco/Routeur/SSH avec un routeur cisco\|SSH avec un routeur cisco]]