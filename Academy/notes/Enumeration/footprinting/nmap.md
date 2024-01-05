# Nmap (Network Mapper) 

definition: open-source network analysis and security auditing tool.

### Use cases:
- Audit security aspects of the network
- Simulate pentests
- Check firewall and IDS settings/configurations
- Types of possible connections
- Network mapping
- Response analytics
- Identify open ports
- Vulnerability assesment

## Host Enumeration

### Host Discovery
We should start by getting an overview of which systems are online. The most effective host discovery method is to use ICMP echo requests.<br>
```Shell
sudo nmap -sn -PE --packet-trace --disable-arp-ping -oA icmp_scan 10.129.2.18
```
| Flag | Description |
| ----------- | ----------- |
| -sn | disable port scanning |
| -PE | perform ping scan using ICMP Echo requests | 
| --packet-trace | shows all packets sent and received | 
| --disable-arp-ping | ensure nmap doesnt use ARP pings | 
| -oA icmp_scan | store results in all formats with name 'icmp_scan' |

**NOTE:** this scanning method only works if the firewalls of the hosts allow it, otherwise, we can use firewall and IDS/IPS evasion techniques.

### Host and Port Discovery
Once we know a target is alive, we can start gathering more information such as:
 - Open ports and their services
 - service versions
 - information that these services provide
 - operating systems

Port states will be defined as follows:<br>
| State | Description |
| ----- | ----------- |
| open  | This indicates that the connection to the scanned port has been established. These connections can be TCP connections, UDP datagrams as well as SCTP associations. |
| closed | When the port is shown as closed, the TCP protocol indicates that the packet we received back contains an RST flag. This scanning method can also be used to determine if our target is alive or not.|
| filtered | Nmap cannot correctly identify whether the scanned port is open or closed because either no response is returned from teh target for the port or we get an error code from the target. | 
| unfiltered | This state of a port only occurs during the TCP-ACK scan and means that the port is accessible, but it cannot be determined whether it is open or closed. | 
| open\filtered | If we do not get a response for a specific port. Indicates that a firewall or packet filter may protect the port. |
| closed\filtered | This state only occurs in the IP ID idle scans and indicates that it was impossible to determine if the scanned port is closed or filtered by a firewall. | 


 ### Saving the Results
It is best practice to save the results of each scan. This is useful not only for reference but also for documentation. Nmap allows us to easily save the results of a scan using three possible formats:<br>
- oN: Normal output, .nmap file extension
- oG: Grepable output, .gnmap file extension
- oX: XML output, .xml file extension. (we can use tools such as xsltproc to transfer our xml to html to have easy to read reports)
<br>OR<br>
- oA: Creates 3 files, one of each type

### Service Enumeration
An essential part of the process, the more information we have, the easier it will be to find known vulnerabilities or find the source code to analyze it.<br>
 - sV: performs service version detection.


### Nmap Scripting Engine (NSE)
| Category | Description | 
| -------- | ----------- | 
| auth | Determination of authentication credentials |
| broadcast | Scripts, which are used for host discovery by broadcasting and the discovered hosts, can be automatically added to the remaining scans. |
| brute | Executes scripts that try to log in to the respective service by brute-forcing credentials | 
| default | Default scripts executed by using the -sC option | 
| discovery | Evaluation of accessible services | 
| dos | These scripts are used to check services for denial of service vulnerabilities and are used less as it harms the services. |
| exploit | This category of scripts tries to exploit known vulnerabilities for the scanned port.|
| external | Scripts that use external services for further processing |
| fuzzer | This uses scripts to identify vulnerabilities and unexpected packet handling by sending defferent fields, which can take much more time | 
| intrusive | Intrusive scripts that could negatively affect the target system |
| malware | Check if some malware infects the target system | 
| safe | Defensive scripts that do not perform intrusive and destructive access. | 
| version | Extension for service deitection. | 
| vuln | Identification of specific vulnerabilities | 

``` Shell
sudo nmap -sC <target> # Default scripts
sudo nmap --script <category> <target>  # Specific scripts category
sudo nmap --script <script-name>, <script-name>, ...  # Defined script(s)
```

All NSE scripts are located at /usr/share/nmap/scripts/. 
We can update this list by running: 
```zsh
sudo nmap --script-updatedb
```

we can also find them with the following command: 
```zsh
find / -type f -name WHAT_WE_LOOKING_FOR* 2>/dev/null | grep scripts
```

### Performance
As the networks we scan become bigger, performance becomes an important factor to consider. We can use certain flags to optimize nmap for our network needs. Some of these are: 
- Which frequency?: --min-parrallelism {number}
- Which timeouts?: --max-rtt-timeout {time}
- How many packets should be sent simultaneously?: --min-rate {number}
- Number of retries?: --max-retries {number}

There are other options as well. Nmap also provides us with timing templates. Using -T flag we can choose from 0 to 5. (0 = Paranoid, 5 = Insane). T3 is default but on a good connection T4 is a solid option according to this article: https://nmap.org/book/performance-timing-templates.html



### Common flags & Usage

``` shell
nmap <scan types> <options> <target>
```

**-h (same as --help)**: Help information. <br>
**-v (same as --verbose)**: by default nmap only prints active, responsive hosts. -v causes nmap to print all hosts and extra info on active ones. **-vv** will provide even more info. <br>
**--reason**: nmap will give a reason to why it is indicating a host as being up <br>

**-p**: allows us to specify a port or port range(ex: -p 443, -p 1-65535). Short hand to scan all ports is **-p-**. More port options exist such as **--top-ports**, **--exclude-ports**, etc... see options for more <br>

**-sn**: disable port scan <br>
**-Pn**: disable ICMP echo requests, treat all hosts as online <br>
**-n**: disable DNS resolution <br>
**--disable-arp-ping**: Disables ARP Ping Requests <br>
**-PE**: performs the ping scan by using ICMP echo requests against the target <br>
**--packet-trace**: shows all packets sent and received <br>

**-T**: determines the speed of the scan (0-5), 0 and 1 are for IDS evasion, 2 slows down the scan to use less bandwidth and target machine resources, 3 is default, 4 speeds up the scan assuming that we are on a reasonably fast and reliable network and 5 assumes we are on an extraordinarily fast network or are willing to scarfice some accuracy for speed. https://nmap.org/book/performance-timing-templates.html

**-oA**: save results in all formats. (**-oN** .nmap, **-oG** .gnmap, **-oX** .xml)<br>

**-sC**: run default scripts<br>
**-sV**: probe open ports to determine service/version info. There are ways to set the 'intensity' (check options)<br>
**-O**: OS detection <br>
**--trace-route**: provides a map of how data is travelling to destination.<br>
**-A**: shorthand to tell nmap to run **-sC, -sV, -O** and **--trace-route** <br>

**--script**: allows us to specify which scripts to run, see above section. <br>

**-sT**: TCP Connect Scan, uses a three-way handshake to determine open or closed. Most accurate way to determine state of a port. Very stealthy as it does not leave any unfinished connections or unsent packets. However, it is slow because it requires scanner to wait for a response from target after each packet sent. Default scan when running without SUDO privileges.<br>
**-sS**: SYN scans, known as "Half-Open" or "Stealth Scan", like -sT however instead of sending an ACK back we send a RST. Requires sudo privileges due to nmap having to craft raw packets. It is the default scan when running sudo nmap.<br>
**-sU**: UDP Scans. Less reliable due to UDP connections being stateless.<br>
**-sN, -sF, -sX**: TCP packets are sent with either no flags set(sN), FIN flag set(sF) or PSH, URG and FIN(sX), we expect a RST packet back if the port is closed. While these are stealthier, we cannot tell with certainty if a port is open. This is because our determining factor is whether or not the target sends a RST packet back. Also, while it is mandated that network hosts respond to malformed packets with a RST TCP packet on closed ports and don't respond at all for open ports this convention is not always respected.<br>

### Useful ressources
https://nmap.org/