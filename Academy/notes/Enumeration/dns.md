# DNS (Domain Name System)
> translate domain names into IP addresses

| Server Types | Description | 
| ------------ | ----------- | 
| DNS Root Server | Responsible for top-level domains (TLD). only requested if the name server does not respond. The *Internet Corporation for Assigned Names and NUmbers* (ICANN) coordinates the work of the root name servers. There are 13 such root servers around the globe. | 
| Authoritative Nameserver | Hold authority for a particular zone. Only answer queries from their area of responsibility. If an authoritative name server cannot answer a clients query, the root name server takes over. | 
| Non-authoritative nameserver | Non-authoritative name servers are not responsible for a particular DNS zone. Instead, they collect information on specific DNS zones themselves, which is done using recursive or iterative DNS querying. | 
| Caching DNS Server | cache information from other name servers for a certain amount of time. The Authorativename server determines the duration of this storage.
| Forwarding Server | perform only one function: They forward DNS queries to another DNS server. |
| Resolver | Not authorative DNS servers but perform name resolution locally in the computer or router. | 


DNS is mainly unencrypted. There are now some solutions for DNS encryption. By default, IT security professionals apply DNS over TLS (DoT) or DNS over HTTPS (DoH) here. In addition, the network protocol DNSCrypt also encrypts the traffic between the computer and the name server.

However, the DNS does not only link computer names and IP addresses. It also stores and outputs additional information about the services associated with a domain.

|DNS Record | Description |
| --------- | ----------- |
| A | Returns an IPv4 address of the requested domain as a result. |
|AAAA | Returns an IPv6 address of the requested domain. |
|MX | Returns the responsible mail servers as a result. |
|NS | Returns the DNS servers (nameservers) of the domain. |
|TXT | This record can contain various information. The all-rounder can be used, e.g., to validate the Google Search Console or validate SSL certificates. In addition, SPF and DMARC entries are set to validate mail traffic and protect it from spam. |
|CNAME | This record serves as an alias. If the domain www.hackthebox.eu should point to the same IP, and we create an A record for one and a CNAME record for the other. |
|PTR | The PTR record works the other way around (reverse lookup). It converts IP addresses into valid domain names. |
|SOA | Provides information about the corresponding DNS zone and email address of the administrative contact. | 


### Cheatsheet
| Command | Description |
| ------- | ----------- | 
| ```dig ns <domain.tld> @<nameserver>``` | NS request to the specific nameserver. | 
| ```dig any <domain.tld> @<nameserver>``` | ANY request to the specific nameserver. | 
| ```dig axfr <domain.tld> @<nameserver>``` | AXFR request to the specific nameserver. | 
| ```dnsenum --dnsserver <nameserver> --enum -p 0 -s 0 -o found_subdomains.txt -f ~/opt/useful/SeclLists/Discovery/DNS/subdomains-top1million.txt <domain.tld>``` [^1]| Subdomain brute forcing.

[^1]: https://github.com/fwaeytens/dnsenum