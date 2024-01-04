# IPMI
> port 623

Intelligent Platform Management Interface (IPMI) is a standardized set of specifications used for managing and monitoring hardware-based host management systems. Operating independently of the host's BIOS, CPU, firmware, and underlying OS, IPMI enables sysadmins to manage and monitor systems even when powered off or unresponsive.

### Functionality
IPMI serves three primary purposes:
- Modifying BIOS settings before OS boot
- Managing fully powered down hosts
- Accessing hosts after system failures

Beyond these tasks, IPMI monitors system temperature, voltage, fan status, and power supplies, queries inventory info, reviews hardware logs, and uses SNMP for alerts.

### Vulnerabilities and Penetration Testing
IPMI is supported by over 200 system vendors. Default credentials for popular BMCs like Dell iDRAC, HP iLO, and Supermicro IPMI are often left unchanged, presenting a significant security risk.

Tools like Metasploit can retrieve IPMI hashes, which, when cracked offline, reveal default or reused passwords. This access can compromise BMCs, granting unauthorized system access or control.

| Command | Description | 
| ------ | ------- | 
| ```msf6 auxiliary(scanner/ipmi/ipmi_version)``` | IPMI version detection. | 
| ```msf6 auxiliary(scanner/ipmi/ipmi_dumphashes)``` | Dump IPMI hashes. |
| ``` sudo nmap -sU --script ipmi-version -p 623 <IP>``` | example of a nmap script to get version | 
