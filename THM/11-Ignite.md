## Info
- Platform: TryHackMe  

---

## Enumeration

### Nmap
<img width="1919" height="885" alt="image" src="https://github.com/user-attachments/assets/f6289e18-a764-4593-a424-8f6fda5faaee" />

- Open ports: 80 (HTTP).

---

### Web Application
<img width="1919" height="828" alt="image" src="https://github.com/user-attachments/assets/1467e92f-45eb-4a39-91b0-1d184c80ea8e" />

- Port 80 was visited and Fuel CMS version 1.4 was discovered.

---

### Searchsploit
<img width="1918" height="853" alt="image" src="https://github.com/user-attachments/assets/05e5460d-1dd8-44c4-bc88-74215138d46e" />

- Exploit `50477.py` for Fuel CMS 1.4.1 Remote Code Execution was discovered and used.

---

## Exploitation
<img width="618" height="172" alt="image" src="https://github.com/user-attachments/assets/ea070be4-aa60-4257-af1a-ca8f908f7e03" />

- `50477.py` was used to obtain access to the target
- Access was obtained as `www-data`.

---

### Netcat Reverse Shell
Netcat listener was started:
```bash
nc -lvnp 4444
```

<img width="1294" height="99" alt="image" src="https://github.com/user-attachments/assets/cb065722-ef36-4e1f-801e-a6f9c597f558" />

- Reverse shell payload was triggered
- Reverse shell as `www-data` was obtained.

---

### First Flag
<img width="452" height="118" alt="1" src="https://github.com/user-attachments/assets/05ec416a-3cb4-4ac8-bd37-d9c24cacfbbb" />

- Flag found: `[FLAG FOUND]`

---

## Privilege Escalation

### Database Configuration
<img width="930" height="255" alt="image" src="https://github.com/user-attachments/assets/ab88bd2d-908e-43ca-8614-09ad1ac8ab87" />

- Fuel CMS database configuration was discovered in `database.php`
- Root credentials were discovered:

<img width="756" height="621" alt="image" src="https://github.com/user-attachments/assets/dd84ddab-3dc9-4c96-8d46-276d82d24978" />

---

### Second Flag
<img width="466" height="175" alt="1" src="https://github.com/user-attachments/assets/65fe8977-da5d-48ea-a892-2a948351b780" />

- Root access was obtained using the discovered credentials.
- Flag found: `[FLAG FOUND]`
