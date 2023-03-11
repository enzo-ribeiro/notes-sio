---
{"dg-publish":true,"permalink":"/cisco/donner-une-priorite-a-un-port-qo-s/"}
---

```IOS
SW-RIB>en
SW-RIB#
SW-RIB#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
SW-RIB(config)#interface fastEthernet 0/1
SW-RIB(config-if)#mls qos ?
  cos            cos keyword
  dscp-mutation  dscp-mutation keyword
  trust          trust keyword

SW-RIB(config-if)#mls qos cos ?
  <0-7>     class of service value between 0 and 7
  override  override keyword

SW-RIB(config-if)#mls qos cos 7
SW-RIB(config-if)#
```
