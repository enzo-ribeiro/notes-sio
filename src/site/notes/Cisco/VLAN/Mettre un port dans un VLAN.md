---
{"dg-publish":true,"permalink":"/cisco/vlan/mettre-un-port-dans-un-vlan/"}
---

```IOS
Switch> en 
Switch# conf t
Switch(config)# int f0/1
Switch(config)# switchport mode access
Switch(config)# switchport access vlan <Numéro_de_VLAN> 
```

// OU

# Mettre plusieurs ports dans un VLAN 

```IOS
Switch> en 
Switch# conf t
Switch(config)# int range f0/1
Switch(config)# switchport mode access
Switch(config)# switchport access vlan <Numéro_de_VLAN> 
```