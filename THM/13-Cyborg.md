## Info
- Platform: TryHackMe  

---

## Enumeration

### Nmap
<img width="1516" height="622" alt="image" src="https://github.com/user-attachments/assets/82852eda-f933-4886-be62-bb6815183e38" />

- Open ports: 22 (SSH) and 80 (HTTP).

---

### Gobuster
<img width="1919" height="517" alt="image" src="https://github.com/user-attachments/assets/e8200a10-ac0f-4a9c-93d9-7a62ae08af7d" />

- `/admin` directory was found.

---

## Exploitation
<img width="1919" height="759" alt="image" src="https://github.com/user-attachments/assets/f5d3650c-4264-4bcb-8417-ddf2aaf4333b" />

- Visiting `/admin` displayed an Admin Shoutbox with a message from an employee that mentioned a `music_archive`
<br><br>

<img width="552" height="150" alt="image" src="https://github.com/user-attachments/assets/97aca9c0-712d-4c78-9b81-6989bc23da5a" />

- Browsing the site’s archive section revealed an archive entry and within that archive an md5crypt hash for the `music_archive` was discovered.

---

### Cracking the password
<img width="1379" height="410" alt="image" src="https://github.com/user-attachments/assets/c61efc1f-1581-47b3-81cc-fd24bb5acbdd" />

- The cracked password was found: `squidward`

---

### Downloading & extracting the Borg archive
<img width="961" height="217" alt="image" src="https://github.com/user-attachments/assets/0f1a7bd1-ffa3-4d67-a4b4-a7d6f26129fa" />

- From the site’s archive page a downloadable archive was downloaded to the attacker machine.
- Using Borg the repository was extracted with the cracked passphrase.
<br><br>

<img width="1293" height="440" alt="image" src="https://github.com/user-attachments/assets/94f727e3-7b66-42ed-b0a3-d135a149ddcb" />

- Extraction produced a `home/alex` directory with user files, including `Documents/note.txt`.
- Inside `home/alex/Documents/note.txt` a note with Alex’s password was found.

---

### SSH to Alex & first flag
- Using the retrieved credentials:
```bash
ssh alex@10.10.70.7
password: S3cretP@s3
```
<br><br>
- After logging in as alex, `user.txt` was found in Alex’s home:
<img width="1103" height="146" alt="1" src="https://github.com/user-attachments/assets/a5a58300-ddc9-45af-8cd3-3bab62c35fed" />

- Flag found: `[FLAG FOUND]`

---

## Privilege escalation
- As alex, sudo -l was run and showed:
```bash
User alex may run the following commands on ubuntu:
    (ALL : ALL) NOPASSWD: /etc/mp3backups/backup.sh
```

---

### Inspect & weaponize /etc/mp3backups/backup.sh
- The script referenced backup_files and included operations executed when run as root.
- Adding a line to set the SUID bit on `/bin/bash`:

<img width="1919" height="848" alt="image" src="https://github.com/user-attachments/assets/aa53e1b1-c0d0-4468-a768-0027950cc1f0" />

- The file permissions were updated so Alex could edit, the change was saved, then the script was executed via sudo.

---

### Obtain root shell & Second Flag
- After the sudoed script executed and `/bin/bash` had the SUID bit set, a root shell was obtained by running:
```bash
/bin/bash -p
```
<br><br>
<img width="565" height="66" alt="1" src="https://github.com/user-attachments/assets/4a297bc7-800c-4f1a-a6da-7d9f4f5cf475" />

- Flag found: `[FLAG FOUND]`
