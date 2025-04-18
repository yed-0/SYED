# 🔐 Network Protocol Vulnerability Lab Walkthrough

**Name:** Syed Muhammad Sajjad 

**Target Machine:** Metasploitable 2 (`192.168.100.131`)  


---

## 🎯 Objective
Explore vulnerabilities in common protocols (FTP, TELNET, SSH, HTTP) via brute-force attacks and network sniffing. Analyze security flaws and propose mitigations.

---
First of all get the ip for our victim which is metasploitable 2.

![image](https://github.com/user-attachments/assets/d5a91d2f-1ef7-49ac-b70b-bca53901c591)

use ip a command.

so here our target ip is 192.168.100.131
## 🔮 1. Enumeration

### Tool Used:
- Nmap

### Command:
```bash
nmap -sS -sV 192.168.100.131
```
use this command on kali :)

![image](https://github.com/user-attachments/assets/a5b52866-3776-4fa3-b9d2-ecf55a82b130)


### Discovered Open Ports & Services:
- FTP (21)
- SSH (22)
- TELNET (23)
- HTTP (80)
- Others (Samba, MySQL, etc.)

we have to get the username in order to launch attack.
So here we can use samba port to get it ><


WHAT IS SAMBA PORT?
-----------------------------------------------------------
Samba is an open-source implementation of theSMB (Server Message Block) protocol
used for file and printer sharing between systems, especially between Linux and Windows.

HOW TO USE IT?
----------------------
enum4linux -U 192.168.100.131 

![image](https://github.com/user-attachments/assets/fa5186a8-b64e-4795-bd1b-4e2c80ba1b48)


### Usernames Found:
From enum4linux :
- msfadmin
- postgres
- root
- ftp
- telnetd
- user

---

## 🔧 2. Brute Force Attacks

### ✅ FTP
**Tool:** Medusa  
**Command:**
```bash
medusa -h 192.168.100.131 -u msfadmin -P passwords.txt -M ftp
```
we need to create password.txt which will be list of password we use to bruteforce.

![image](https://github.com/user-attachments/assets/232bdb41-7f2b-4019-96e6-6f546d35f3eb)

![image](https://github.com/user-attachments/assets/d7ae1f3a-2b78-445f-896f-8ec37ee58103)

now we can use the command to bruteforce ftp port :)

![image](https://github.com/user-attachments/assets/259ff710-ce32-44a7-bd5d-62311701752f)

YEAYYY!!!
### ✅ TELNET
**Tool:** Hydra

**Command:**
```bash
hydra -l msfadmin -P passwords.txt 192.168.100.131 telnet
```

as Hydra is often more reliable with Telnet we will use it.

![image](https://github.com/user-attachments/assets/913775ce-e25f-4035-9301-504aa03408ed)

we can see from the result that the valid password is "msfadmin" ><

### ✅ SSH
**Tool:** NetExec  
**Command:**
```bash
nxc ssh 192.168.100.131 -u username.txt -p passwords.txt
```
SSH Brute Force using NetExec
✅ Step 1: Create a new list for username and save it as username.txt

![image](https://github.com/user-attachments/assets/02d161e2-cb7d-4c88-b18e-19cd328daea4)


now we can use the command to bruteforce SSH  >< :)


![image](https://github.com/user-attachments/assets/7ef51a40-a716-428a-923a-f4c446d8e599)


![image](https://github.com/user-attachments/assets/89f83e58-970f-4b18-b4cd-ad16819a6f7f)





### ✅ HTTP Login (DVWA)
**Tool:** Burp Suite Intruder
- Target: 192.168.100.131
- Payload: Use common user/password list








✅ Step-by-Step Walkthrough:
1. Configure Proxy
Open Burp Suite.Go to the target tab and click "open browser".

![image](https://github.com/user-attachments/assets/f8402202-01e8-4468-b51e-078418d4eb95)





2. Capture HTTP Login Request
Navigate to the login page and login using "admin" "password".


![image](https://github.com/user-attachments/assets/1899208a-cc12-4a53-9e37-bb86b6b6b536)


Enable "Intercept is ON" in Burp → Proxy tab.

![image](https://github.com/user-attachments/assets/945f16f0-0563-4bbd-a8d9-8e985322bcdb)


Now we  move to the bruteforce tab Then enter any username or pass

![image](https://github.com/user-attachments/assets/9bcebb48-22be-4001-b865-1281a018e81e)



Burp will intercept the GET request:
right click on the GET reqquest and choose send to intruders.

![image](https://github.com/user-attachments/assets/e1068557-6727-41af-aa77-d648ec2f6313)


3. Set Payload Positions
Go to the Intruder tab → Positions.

Highlight the username and password values:
it should look something like "username=§admin§&password=§1234§&Login=Login".Add both to payload.Set Attack Type to Cluster Bomb.


![image](https://github.com/user-attachments/assets/4938290d-be28-41ed-9836-63ec45052b31)




4. Configure Payloads
Go to the Payloads tab.

Payload Set 1: Usernames

Add common usernames.

![image](https://github.com/user-attachments/assets/b885cef1-236f-4d4a-99bc-8a9e24871fdd)



Payload Set 2: Passwords

Add common passwords.You may use custom or default wordlists.

![image](https://github.com/user-attachments/assets/09745cb7-1f5c-4f21-a846-78186f742c04)


5. Launch the Attack
Click Start attack.


6. Analyze Results

Right click the most max value of length and choose "show response in browser" then click copy.


![image](https://github.com/user-attachments/assets/fab7d799-8eff-4ac1-b073-9d5177618423)


![image](https://github.com/user-attachments/assets/078cb148-a8a4-43eb-935e-1ab9b6c656f4)


paste it in the browser and you should success!

![image](https://github.com/user-attachments/assets/3e75c60a-4b3c-4c97-aa59-7cc308d76549)





### ✅Wireshark Traffic Analysis:  Credential Transmission Across Protocols

## Tools Used
Tools: Wireshark

Target machine: 192.168.100.131

Attacker machine: kali

## 1. Capturing FTP Credentials
Procedure:
Launch Wireshark and start capturing on your active network interface

In your terminal, connect to the FTP service: (ftp 192.168.100.131)


![image](https://github.com/user-attachments/assets/f138e5bf-d857-48e3-9744-bd0fadc2a9c2)

In Wireshark, apply the filter: "ftp || tcp.port == 21"

![image](https://github.com/user-attachments/assets/1a333376-8ce1-4417-8470-47fc3e2572ac)


Locate a packet with USER msfadmin in the Info column


![image](https://github.com/user-attachments/assets/e2107f79-bb44-49f3-a654-99148a345159)



Right-click → Follow → TCP Stream to view the complete session


![image](https://github.com/user-attachments/assets/3a6ef18d-aefb-4b33-9a69-b385e9e7b242)



### 2. Capturing TELNET Credentials
## Procedure:
In your terminal, connect to the TELNET service:"telnet 192.168.100.131"


![image](https://github.com/user-attachments/assets/2c65e88e-a27f-40e7-afb5-b0a67efad4f3)


In Wireshark, apply the filter:"telnet || tcp.port == 23"
Examine the packet list for TELNET traffic.
Right-click → Follow → TCP Stream to view the session.


![image](https://github.com/user-attachments/assets/ebf2e7d2-322c-4c81-b819-7ef910b8d6c6)


### 3. Analyzing SSH Traffic
## Procedure:
Initiate an SSH session:"ssh -oHostKeyAlgorithms=+ssh-rsa -oPubkeyAcceptedKeyTypes=+ssh-rsa msfadmin@192.168.100.131"


![image](https://github.com/user-attachments/assets/32a14aef-d32a-4c26-9f95-8bd4dbb1f9f8)

In Wireshark, apply the filter:"ssh || tcp.port == 22"


![image](https://github.com/user-attachments/assets/b9728d00-03f8-4748-9a46-96c5840bbbf5)



Examine the captured SSH packets and we are good enough :)

![image](https://github.com/user-attachments/assets/04429230-8084-4e15-9a8b-87a0343c1662)


![image](https://github.com/user-attachments/assets/90bd1f50-5819-450b-b19f-db3adb5c7222)





