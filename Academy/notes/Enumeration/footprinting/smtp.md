# SMTP (Simple Mail Transfer Protocol)
>protocol for sending emails in an ip network. <br>
>common ports: 25(SMPT), 587(SMTPS) 465(outdated implementation of SMTPS). 

After sending an email SMTP Client (MUA - Mail User Agent) converts it into a header and a body and uploads both the the SMTP server. This has a Mail Transfer Agent(MTA) which checks the email for size and spam and then stores it. Sometimes, to relieve it, it is sometimes preceded by a Mail Submission Agent (MSA) which checks the valididty. MSA are also called Relay servers. The MTA then searches the DNS for the IP of the recipient mail server. On arrival at the recipient SMTP server the data packets are reassembled, from there, the Mail Delivery Agent (MDA) transfers it to the recipient mailbox.

Client (MUA) ➞ Submission Agent (MSA) ➞ Open Relay (MTA) ➞ Mail Delivery Agent (MDA) ➞ Mailbox (POP3/IMAP)
<br><br>

Use telnet to connect to SMTP servers, some useful commands are:
| Command |Description |
| ------- | ---------- |
| AUTH PLAIN | AUTH is a service extension used to authenticate the client. |
| HELO | The client logs in with its computer name and thus starts the session. |
| MAIL FROM | he client names the email sender. |
| RCPT TO | The client names the email recipient. |
| DATA | The client initiates the transmission of the email. |
| RSET | The client aborts the initiated transmission but keeps the connection between client and server. |
| VRFY | The client checks if a mailbox is available for message transfer. |
| EXPN | The client also checks if a mailbox is available for messaging with this command. |
| NOOP | The client requests a response from the server to prevent disconnection due to time-out. |
| QUIT | The client terminates the session. |


# Cheatsheet
| Command | Description | 
| ------- | --------- |
| ```telnet <FQDN/IP> 25``` | Connect to the SMTP server| 
| ```sudo nmap <FQDN/IP> -p25 --script smtp-open-relay -v```[^1]| Attempts to relay mail by issuing a predefined combination of SMTP commands. |
| ```smtp-user-enum -M VRFY -U <wordlist> -t <IP>``` | Enum users |

[^1]: https://nmap.org/nsedoc/scripts/smtp-open-relay.html