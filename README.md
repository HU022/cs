# CS
Welcome to CS list.
# Preparation
- Create Kali Linux VM
- Create Nessus VM (https://www.tenable.com/try)
# Basic steps

 1. Ping test
 2. Nmap test
 3. Based on open ports in Nmap scan, find vulnerabilitys. With port 80 or 443, a website is running

# NMAP
**Nmap verbose scan, runs syn stealth, T4 timing (should be ok on LAN), OS and service version info, traceroute and scripts against services**
`nmap -v -sS -A -T4 target`

**As above but scans all TCP ports (takes a lot longer)**
`nmap -v -sS -p- -A -T4 target`

**As above but scans all TCP ports and UDP scan (takes even longer)**
`nmap -v -sU -sS -p- -A -T4 target`

**Search nmap scripts for keywords**
`ls /usr/share/nmap/scripts/* | grep ftp`

**Nmap script to scan for vulnerable SMB servers - WARNING: unsafe=1 may cause knockover**
`nmap -v -p 445 --script=smb-check-vulns --script-args=unsafe=1 target`


## Specific services
**Port 21 - FTP**
`nmap --script ftp-anon,ftp-bounce,ftp-libopie,ftp-proftpd-backdoor,ftp-vsftpd-backdoor,ftp-vuln-cve2010-4221,tftp-enum -p 21 <TARGET_IP>`

**Port 25 - SMTP**
`nmap --script=smtp-commands,smtp-enum-users,smtp-vuln-cve2010-4344,smtp-vuln-cve2011-1720,smtp-vuln-cve2011-1764 -p 25 <TARGET_IP>`
`smtp-user-enum -M VRFY -U /root/sectools/SecLists/Usernames/Names/names.txt -t <TARGET_IP>`

**Port 69 - UDP - TFTP**
`nmap -p69 --script=tftp-enum.nse 10.11.1.111

**Port 88 - Kerberos**
`nmap -p 88 --script=krb5-enum-users --script-args="krb5-enum-users.realm='DOMAIN.LOCAL'" <TARGET_IP>`

**Port 135 - MSRPC**
`nmap target --script=msrpc-enum`

**Port 139/445 - SMB**
`nmap --script=smb-enum* --script-args=unsafe=1 -T5 <TARGET_IP>
nmap --script smb-enum-shares -p139,445 -T4 -Pn <TARGET_IP>
nmap --script smb-vuln* -p139,445 -T4 -Pn <TARGET_IP>
nmap -p445 --script smb-brute --script-args userdb=userfilehere,passdb=/usr/share/seclists/Passwords/Common-Credentials/10-million-password-list-top-1000000.txt <TARGET_IP> -vvvv
nmap –script smb-brute <TARGET_IP>`

`nmap –script smb-brute <TARGET_IP>`

**Port 161/162 UDP - SNMP**

`nmap -vv -sV -sU -Pn -p 161,162 --script=snmp-netstat,snmp-processes <TARGET_IP>`

**Port 443 - HTTPS**

`nmap -sV --script=ssl-heartbleed <TARGET_IP>`

**Port 1433 - MSSQL**

`nmap -p 1433 -sU --script=ms-sql-info.nse <TARGET_IP>`

**Port 1521 - Oracle**

`nmap -p 1521 -A <TARGET_IP>`

`nmap -p 1521 --script=oracle-tns-version,oracle-sid-brute,oracle-brute <TARGET_IP>`

**Port 3306 - MySQL**

`nmap --script=mysql-databases.nse,mysql-empty-password.nse,mysql-enum.nse,mysql-info.nse,mysql-variables.nse,mysql-vuln-cve2012-2122.nse <TARGET_IP> -p 3306`

 **Port 3389 - RDP**

`nmap -p 3389 --script=rdp-vuln-ms12-020.nse <TARGET_IP>`

 **Port 5900 - VNC**

`nmap --script=vnc-info,vnc-brute,vnc-title -p 5900 <TARGET_IP>`

# Nikto
 **To scan a particular host**
`nikto -host [host IP/name]`

 **To scan a host on multiple ports (default = 80)**
`nikto -host [host IP/name] -port [port number 1], [port number 2], [port number 3]`

 **To scan a host and output fingerprinted information to a file**
`nikto -host [host IP/name] -output [output_file]`

**To use a proxy while scanning a host**
`nikto -host [host IP/name] -useproxy [proxy address]`

# Crack Hashes (Crackstation)
https://crackstation.net/

# All in one tool (hashing etc)
- https://gchq.github.io/CyberChef/
- Nessus tenable Vulnerability scanner: https://www.tenable.com/try

# Website

 1. Always check websites for 'robots.txt. 
## Wordpress scanner
**Basic scan**
`wpscan --url example.com`
**Password brute force attack**
`wpscan --url example.com -e u --passwords /path/to/password_file.txt`
 
# Other CS
 1. https://github.com/Kitsun3Sec/Pentest-Cheat-Sheets
 2. https://github.com/coreb1t/awesome-pentest-cheat-sheets
 3. https://github.com/qazbnm456/awesome-web-security/blob/master/README.md
 4. https://github.com/andrewjkerr/security-cheatsheets
