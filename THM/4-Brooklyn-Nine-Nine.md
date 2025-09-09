## Info
- Platform: TryHackMe  
- Difficulty: Easy  

---

## Enumeration

### Nmap
```bash
nmap -sV -sC -O 10.10.92.211
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-09 08:09 EDT
Nmap scan report for 10.10.92.211
Host is up (0.070s latency).
Not shown: 997 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.21.4.114
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 2
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 0        0             119 May 17  2020 note_to_jake.txt
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 16:7f:2f:fe:0f:ba:98:77:7d:6d:3e:b6:25:72:c6:a3 (RSA)
|   256 2e:3b:61:59:4b:c4:29:b5:e8:58:39:6f:6f:e9:9b:ee (ECDSA)
|_  256 ab:16:2e:79:20:3c:9b:0a:01:9c:8c:44:26:01:58:04 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.4.29 (Ubuntu)
Device type: general purpose
Running: Linux 4.X
OS CPE: cpe:/o:linux:linux_kernel:4.15
OS details: Linux 4.15
Network Distance: 2 hops
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.63 seconds
```
- Open ports: 21 (FTP), 22 (SSH), 80 (HTTP).

---
<img width="513" height="299" alt="Screenshot_2025-09-09_08-13-07" src="https://github.com/user-attachments/assets/360931f7-65c1-43dc-90a7-c2365245c166" />

- FTP allows **anonymous login**.  
- File found: `note_to_jake.txt`.

---

## FTP & Information Disclosure
<img width="1428" height="176" alt="Screenshot_2025-09-09_08-16-06" src="https://github.com/user-attachments/assets/71410704-ecea-466c-97ea-4a5c3743ef1a" />

- Anonymous login successful.  
- `note_to_jake.txt` reveals that user **jake** has a weak password.

---

## Exploitation
<img width="1909" height="446" alt="image" src="https://github.com/user-attachments/assets/62560c4e-84ea-411a-8146-86e61d5bcfe0" />

- Brute forced SSH with Hydra.  
- Valid credentials found:  
- Username: `jake`  
- Password: `987654321` 

---

<img width="1096" height="606" alt="image" src="https://github.com/user-attachments/assets/c88ff041-c957-45cd-9013-a2c0d01e9a8f" />

- SSH access gained as `jake`.  
- User flag located in `/home/holt/user.txt`.

---

## Privilege Escalation
<img width="1629" height="751" alt="image" src="https://github.com/user-attachments/assets/3d5073c8-7e4d-49c3-a5c5-80b2cb133e74" />

- `sudo -l` shows that **less** can be run as root without password.  
- Exploited with `sudo less /etc/passwd` → `!bash`.  
- Root shell obtained.
- Root flag captured

