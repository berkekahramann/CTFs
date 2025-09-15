## Info
- Platform: TryHackMe  
- Difficulty: Easy

---

## Enumeration

### Nmap
<img width="1354" height="496" alt="Screenshot_2025-09-15_07-51-01" src="https://github.com/user-attachments/assets/4e5ebf3c-d71b-4094-823f-3a5300071568" />

- Open ports: 22 (SSH), 80 (HTTP).

---

### Gobuster
```bash
gobuster dir -u http://10.10.27.133 -w /usr/share/wordlists/dirb/common.txt -x php,txt,html
===============================================================
Gobuster v3.8
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.27.133
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8
[+] Extensions:              txt,html,php
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.hta.txt             (Status: 403) [Size: 277]
/.hta.html            (Status: 403) [Size: 277]
/.hta                 (Status: 403) [Size: 277]
/.htaccess.php        (Status: 403) [Size: 277]
/.htaccess            (Status: 403) [Size: 277]
/.hta.php             (Status: 403) [Size: 277]
/.htaccess.txt        (Status: 403) [Size: 277]
/.htpasswd            (Status: 403) [Size: 277]
/.htpasswd.php        (Status: 403) [Size: 277]
/.htaccess.html       (Status: 403) [Size: 277]
/.htpasswd.txt        (Status: 403) [Size: 277]
/.htpasswd.html       (Status: 403) [Size: 277]
/css                  (Status: 301) [Size: 310] [--> http://10.10.27.133/css/]
```
/index.php            (Status: 200) [Size: 616]
/index
