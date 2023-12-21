# NFS (Network File System)
> purpose: access file systems over a network as if they were local <br>
> common ports: 111(portmapper, nfsv3) and 2049 (nfs server)

NFS is based on the Open Network Computing Remote Procedure Call (ONC-RPC/SUN-RPC) protocol exposed on TCP and UDP ports 111, which uses External Data Representation (XDR) for the system-independent exchange of data.

A significant advantage of NFSv4 over its predecessors is that only one UDP or TCP port 2049 is used to run the service, which simplifies the use of the protocol across firewalls.

### Cheatsheet
| Command | Description |
| ------- | ----------- |
|```showmount -e <FQDN/IP>``` | Show available NFS shares. |
| ```mount -t nfs <FQDN/IP>:/<share> ./target-NFS/ -o nolock ```|	Mount the specific NFS share.  (After mounting usefule to run tree in the directory)|
|``` umount ./target-NFS``` | Unmount the specific NFS share.|
|```sudo nmap --script nfs* <IP> -sV -p111,2049``` | run nmap nfs scripts