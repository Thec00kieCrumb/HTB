# FTP (File Transfer Protocol)
>used for the transfer of computer files from a server to a client on a computer network. <br>
>Common ports: 20(data channel), 21(control channel) 

The File Transfer Protocol (FTP) is one of the oldest protocols on the Internet. The FTP runs within the application layer of the TCP/IP protocol stack. Thus, it is on the same layer as HTTP or POP. 

 - FTP is a clear-text protocol that can sometimes be sniffed if conditions on the network are right
 - FTP usually requires credentials
 - possibility that a server offers anonymous FTP. The server operator then allows any user to upload or download files via FTP without using a password options for users are usually limited


### Default Configuration

One of the most used FTP servers on Linux-based distributions is vsFTPd. The default configuration of vsFTPd can be found in /etc/vsftpd.conf, and some settings are already predefined by default. It is highly recommended to install the vsFTPd server on a VM and have a closer look at this configuration.

```shell
sudo apt install vsftpd 
```

### Cheatsheet
| Command | Description | 
| ------- | ----------- | 
| ```ftp <FQDN/IP>``` | Interact with the FTP service on the target. | 
| ```nc -nv <FQDN/IP> 21``` | Interact with the FTP service on the target. | 
| ```telnet <FQDN/IP> 21``` |  	Interact with the FTP service on the target. | 
| ```openssl s_client -connect <FQDN/IP>:21 -starttls ftp``` | Interact with the FTP service on the target using encrypted connection. |
| ```wget -m --no-passive ftp://anonymous:anonymous@<target>``` | Download all available files on the target FTP server.(Loud) | 


### Useful ressources
https://en.wikipedia.org/wiki/List_of_FTP_server_return_codes