# MSSQL (Microsoft SQL)

Microsoft SQL (MSSQL) is a closed-source relational database system by Microsoft, initially designed for Windows OS. It's favored in .NET framework applications due to its native support for .NET. The system includes default databases like master, model, msdb, tempdb, and resource, each serving specific purposes. Authentication is often done via Windows Authentication, connecting through SSMS, which can be installed separately and not just limited to the database server.

Admins might make configuration errors due to time pressure, leading to vulnerabilities such as unencrypted connections, self-signed certificates, default sa credentials, or using named pipes. Footprinting involves using tools like NMAP and Metasploit to scan for MSSQL service details and potential vulnerabilities.

MSSQL can be interacted with using various clients like Impacket's mssqlclient.py, enabling interaction with databases using Transact-SQL. This allows exploration and management of databases once connected.


### Cheatsheet
| Command | Description |
| ------ | ---------- | 
| ```mssqlclient.py <user>@<FQDN/IP> -windows-auth``` | Log in to the MSSQL server using Windows authentication. |
| ```sudo nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 <IP>``` | nmap scripted scan to gather information such as hostname, database instance name, software version, etc... |
| ```msf> use auxiliary/scanner/mssql/mssql_ping``` | msfconsole to enumerate basic info