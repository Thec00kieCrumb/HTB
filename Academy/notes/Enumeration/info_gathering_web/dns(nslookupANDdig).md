## DNS Overview

The Domain Name System (DNS) serves as the internet's phone book, translating human-readable domain names into IP addresses that computers understand.

### What is DNS?

DNS translates domain names like `hackthebox.com` to IP addresses like `104.17.42.72`, enabling browsers to access internet resources.

Advantages of DNS:
- Names instead of numbers for hosts (Easier recall/nicer looking for humans:))
- Server numeric address changes without notifying everyone
- Single name referring to multiple hosts

### Resource Records


| Resource Record     | Description|
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| A domain name| The first part of a Resource Record, typically a fully qualified domain name. If not fully qualified, the zone's name where the record is located is appended.|
| TTL| Time-To-Live (TTL) in seconds. Defaults to the minimum value specified in the SOA record.|
| Record Class| Can be Internet, Hesiod, or Chaos.|
| Start Of Authority| Indicates the start of a zone file and includes zone values like a serial number and multiple expiration timeouts.|
| Name Servers (**NS**)| NS Records bind the distributed database, managing a zone's authoritative name server and the authority for a child zone to a name server.|
| IPv4 Addresses (**A**) | A record mapping between a hostname and an IP address. 'Forward' zones utilize A records.|
| Pointer (**PTR**)| PTR record maps an IP address to a hostname. 'Reverse' zones contain PTR records.|
| Canonical Name (**CNAME**) | Maps an alias hostname to an A record hostname using the CNAME record.|
| Mail Exchange (**MX**)  | Identifies a host that accepts emails for a specific host, with assigned priority values. Multiple MX records can exist, forming a prioritized list for a host.|


### Cheatsheet

| Command                               | Description                                        |
|---------------------------------------|----------------------------------------------------|
| nslookup $TARGET                      | Identify the A record for the target domain.       |
| nslookup -query=A $TARGET             | Identify the A record for the target domain.       |
| dig $TARGET @<nameserver/IP>          | Identify the A record for the target domain.       |
| dig a $TARGET @<nameserver/IP>        | Identify the A record for the target domain.       |
| nslookup -query=PTR <IP>              | Identify the PTR record for the target IP address.  |
| dig -x <IP> @<nameserver/IP>          | Identify the PTR record for the target IP address.  |
| nslookup -query=ANY $TARGET           | Identify ANY records for the target domain.        |
| dig any $TARGET @<nameserver/IP>      | Identify ANY records for the target domain.        |
| nslookup -query=TXT $TARGET           | Identify the TXT records for the target domain.    |
| dig txt $TARGET @<nameserver/IP>      | Identify the TXT records for the target domain.    |
| nslookup -query=MX $TARGET            | Identify the MX records for the target domain.     |
| dig mx $TARGET @<nameserver/IP>       | Identify the MX records for the target domain.     |
