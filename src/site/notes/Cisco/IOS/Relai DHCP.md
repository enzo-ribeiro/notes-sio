---
{"dg-publish":true,"permalink":"/cisco/ios/relai-dhcp/"}
---

Un relay DHCP va servir à faire passer un réseau au DHCP.
Pour ca il nous faut donc un serveur DHCP ainsi que plusieurs réseaux.

```IOS
Switch>en
Switch#conf t
Switch(config)#ip dhcp relay enable
```
 Notre relais est activé maintenant il faut déclarer le serveur DHCP.
```IOS
Switch(config)#ip dhcp relay address <@_IP_serveur_DHCP>
```
