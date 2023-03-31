---
{"dg-publish":true,"permalink":"/cisco/ios/relai-dhcp/"}
---

Un relay DHCP va servir à faire passer un réseau au DHCP.
Pour ca il nous faut donc un serveur DHCP ainsi que plusieurs réseaux.

```IOS
Routeur>en
Router#conf t
Routeur(config)#hostname RT-RIB
RT-RIB(config)#int <interface_voulu>
RT-RIB(config)#ip helper-address <@_IP_serveurDHCP>
```
