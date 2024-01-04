# Oracle TNS

### Overview
Oracle TNS (Transparent Network Substrate) facilitates communication between Oracle databases and applications over networks. Initially part of the Oracle Net Services suite, TNS supports various networking protocols and is vital in managing large databases in industries like healthcare, finance, and retail. Its encryption ensures data security in enterprise environments.

### Capabilities
- Supports IPv6, SSL/TLS encryption, aiding in name resolution, connection management, load balancing, and security.
- Provides encryption for client-server communication over TCP/IP, securing data transmission.
- Offers tools for performance monitoring, analysis, error reporting, workload management, and fault tolerance.

### Default Configuration
- Default settings vary based on the Oracle software version and edition.
- Listener typically operates on TCP/1521 but can be altered.
- Supports multiple network protocols, interfaces, and security features.
- Uses `tnsnames.ora` and `listener.ora` files for configurations.

### Usage and Configuration
- Utilized with various Oracle services like databases, enterprise managers, web servers, etc.
- `tnsnames.ora` contains entries for connecting to services.
- `listener.ora` defines listener properties and parameters for incoming requests.

### Interaction and Enumeration
- Tools like ODAT, nmap, and sqlplus help interact and enumerate Oracle databases.
- Enumerating SIDs (System Identifiers) aids in connecting to specific database instances.
- Extracting password hashes, database enumeration, and file uploads are possible post-access.


### Cheatsheet 

| Command | Description | 
| ------- | ----------- |
| ```sudo nmap -p1521 -sV <IP> --open --script oracle-sid-brute``` | use NMAP to guess SIDs|
| ```./odat.py all -s <IP>``` | use odat.py to scan for db names, versions, running processes, user accounts, vulns, misconfigurations, etc... | 
| ```sqlplus <USER>/<Password>@<IP>/<SID>``` | interact with the Oracle database | 


ressource to checkout : https://book.hacktricks.xyz/network-services-pentesting/1521-1522-1529-pentesting-oracle-listener