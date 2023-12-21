# SNMP (Simple Network Management Protocol)
>was created to monitor network devices. In addition, this protocol can also be used to handle configuration tasks and change settings remotely. SNMP-enabled hardware includes routers, switches, servers, IoT devices, and many other devices that can also be queried and controlled using this standard protocol.<br>
> Port: 161, 162


MIB (Management Information Base) is a text file which all queryable SNMP objects of a device are listed in a standardized tree hierarchy.

SNMPv1 has no built-in authentication mechanism, meaning anyone accessing the network can read and modify network data. Another main flaw of SNMPv1 is that it does not support encryption, meaning that all data is sent in plain text and can be easily intercepted.

Regarding security, SNMPv2 is on par with SNMPv1. v2c is a version that still exists today and the extension c means community based SNMP. However, a significant problem with the initial execution of the SNMP protocol is that the community string that provides security is only transmitted in plain text, meaning it has no built-in encryption.

SNMPv3 has security features such as authentication and encryption. However, the complexity also increases to the same extent, with significantly more configuration options than v2c.



### Cheatsheet
| Commands | Description | 
| -------- | ----------- |
| ```snmpwalk -v2c -c <community string> <FQDN/IP>``` | Querying OIDs using snmpwalk. |
| ```onesixtyone -c community-strings.list <FQDN/IP>``` | Bruteforcing community strings of the SNMP service. |
| ```braa <community string>@<FQDN/IP>:.1.* ```[^1]| Bruteforcing SNMP service OIDs. |

[^1]: https://github.com/mteg/braa