# SMB (Server Message Block)
>client-server protocol that regulates access to files and entire directories and other network resources (such as printers)<br>
Common ports: 137, 138, **139**, **445**

Samba is an alternative variant to the SMB server developed for Unix-based operating system. Default configuration file: /etc/samba/smb.conf

With RPC (Remote Procedure Call) we can gain more information about the server. Refer to man page of rpcclient. Some of these are: srvinfo, enumdomains, querydominfo, netshareenummall, netsharegetinfo < share >, enumdomusers, queryuser < RID >, etc...<Br>
EX:<br>
```shell
user$ rpcclient -U "" TARGETIP
rpcclient$> enumdomains
```

### Useful commands
smbclient is part of the samba suite and let's us interact with SMB shares.<br>
-L let's us list the share <br>
-N is "Null session" (anonymous access without the input of existing users or valid passwords)
``` shell
smbclient -L -N //TARGET_IP
```
--shares can help enumerate the shares but crackmapexec has many more functionality.
```
crackmapexec smb TARGETIP --shares
```

### Cheatsheet

| Command | Description | 
| ------- | ----------- | 
| ```smbclient -N -L \<FQDN/IP>``` | Null Session authentication on SMB. | 
| ```smbclient //<FQDN/IP>/<share>``` | Connect to a specific SMB share |
| ```rpcclient -U "" <FQDN/IP>``` | Interaction with the target using RPC. |
| ```samrdump.py <FQDN/IP>```[^1] | Username enumeration using Impacket scripts. |
| ```smbmap -H <FQDN/IP>``` | Enumerating SMB shares. | 
| ```crackmapexec smb <FQDN/IP> --shares -u '' -p ''``` | Enumerating SMB shares using null session authentication. |
| ```enum4linux-ng.py <FQDN/IP> -A``` [^2] | SMB enumeration using enum4linux. |


[^1]: https://github.com/fortra/impacket
[^2]: https://github.com/cddmp/enum4linux-ng