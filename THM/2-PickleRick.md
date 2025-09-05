## Bilgi
- Platform: TryHackMe  
- Zorluk: Easy

---

## Enumeration

### Nmap
```bash
nmap -sV -O 10.10.53.170
```
<img width="1374" height="484" alt="image" src="https://github.com/user-attachments/assets/453c2d06-8ed6-4f41-a392-27e4c18a5465" />
<pre>Açık portlar: 
22/tcp → SSH (OpenSSH 8.2p1) 
80/tcp → HTTP (Apache 2.4.41) 
</pre>

### Web İnceleme
#### Anasayfa
<img width="1917" height="829" alt="image" src="https://github.com/user-attachments/assets/27e99a22-bcc9-4b90-8517-75c8837597ea" />

#### Kaynak Kod
<img width="1917" height="829" alt="image" src="https://github.com/user-attachments/assets/08b2d02b-5346-4f28-8e90-7fa4bc687c7e" />
```bash
Username: R1ckRul3s
```

### Gobuster
```bash
gobuster dir -u http://10.10.53.170 -w /usr/share/wordlists/dirb/common.txt -x php,html,txt,js,css,sh
===============================================================
Gobuster v3.8
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.53.170
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8
[+] Extensions:              css,sh,php,html,txt,js
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.hta                 (Status: 403) [Size: 277]
/.hta.sh              (Status: 403) [Size: 277]
/.hta.css             (Status: 403) [Size: 277]
/.hta.txt             (Status: 403) [Size: 277]
/.hta.js              (Status: 403) [Size: 277]
/.hta.html            (Status: 403) [Size: 277]
/.hta.php             (Status: 403) [Size: 277]
/.htaccess            (Status: 403) [Size: 277]
/.htaccess.css        (Status: 403) [Size: 277]
/.htaccess.txt        (Status: 403) [Size: 277]
/.htaccess.js         (Status: 403) [Size: 277]
/.htaccess.php        (Status: 403) [Size: 277]
/.htaccess.sh         (Status: 403) [Size: 277]
/.htpasswd            (Status: 403) [Size: 277]
/.htpasswd.html       (Status: 403) [Size: 277]
/.htpasswd.php        (Status: 403) [Size: 277]
/.htaccess.html       (Status: 403) [Size: 277]
/.htpasswd.txt        (Status: 403) [Size: 277]
/.htpasswd.sh         (Status: 403) [Size: 277]
/.htpasswd.js         (Status: 403) [Size: 277]
/.htpasswd.css        (Status: 403) [Size: 277]
/assets               (Status: 301) [Size: 313] [--> http://10.10.53.170/assets/]
/denied.php           (Status: 302) [Size: 0] [--> /login.php]
/index.html           (Status: 200) [Size: 1062]
/index.html           (Status: 200) [Size: 1062]
/login.php            (Status: 200) [Size: 882]
/portal.php           (Status: 302) [Size: 0] [--> /login.php]
/robots.txt           (Status: 200) [Size: 17]
/robots.txt           (Status: 200) [Size: 17]
/server-status        (Status: 403) [Size: 277]
Progress: 32291 / 32291 (100.00%)
```

#### Robots.txt
<img width="1919" height="831" alt="image" src="https://github.com/user-attachments/assets/f2f8d38f-cab6-417f-97bc-344da98accff" />
Buradan "Wubbalubbadubdub" parolası bulundu.
