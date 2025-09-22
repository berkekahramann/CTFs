## Info
- Platform: TryHackMe  

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

---

### Web İnceleme
#### Home Page
<img width="1917" height="829" alt="image" src="https://github.com/user-attachments/assets/27e99a22-bcc9-4b90-8517-75c8837597ea" />

#### Source Code
<img width="1917" height="829" alt="image" src="https://github.com/user-attachments/assets/08b2d02b-5346-4f28-8e90-7fa4bc687c7e" />

Username: R1ckRul3s

---


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

---

#### Robots.txt
<img width="1919" height="831" alt="image" src="https://github.com/user-attachments/assets/f2f8d38f-cab6-417f-97bc-344da98accff" />
The password "Wubbalubbadubdub" was found here.

---

#### Login

Logged in using the username and password:
<img width="1917" height="826" alt="image" src="https://github.com/user-attachments/assets/2c3f11b1-dac0-4805-926d-23dec0e0d968" />

Username: R1ckRul3s
Password: Wubbalubbadubdub

---

### Portal (Command Panel)
#### Flags
<img width="1919" height="759" alt="image" src="https://github.com/user-attachments/assets/9dc3562e-590c-4d56-b6f3-6a917700862a" />

<img width="1919" height="759" alt="image" src="https://github.com/user-attachments/assets/2cb88347-72b9-4807-a917-33fa7b192ee2" />
The 1st ingredient was found in the file "Sup3rS3cretPickl3Ingred.txt".

---


<img width="1919" height="759" alt="image" src="https://github.com/user-attachments/assets/f9f95e2c-88b5-4e71-8a62-a94881ab7cec" />
The 2nd ingredient was found in the /home/rick/"secret ingredients" directory.

---

### Using Sudo 
<img width="1919" height="764" alt="image" src="https://github.com/user-attachments/assets/abcf863b-258f-4583-80ab-22beac9cf545" />

```bash
sudo -l kullanarak sudo kullanmak için şifre gerekmediği görüldü
```

<img width="1919" height="759" alt="image" src="https://github.com/user-attachments/assets/79bf4dee-319b-427c-a6d3-7a5343758b12" />
The 3rd ingredient was found using `sudo less /root/3rd.txt`.
