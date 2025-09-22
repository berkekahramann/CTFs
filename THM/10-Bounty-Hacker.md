## Info
- Platform: TryHackMe  

---

## Enumeration

### Nmap
<img width="1903" height="454" alt="image" src="https://github.com/user-attachments/assets/976ae41c-1fd3-42bc-8927-762abb730649" />

- Open ports: 21 (FTP), 22 (SSH), 80 (HTTP).

---

### FTP
<img width="1919" height="801" alt="image" src="https://github.com/user-attachments/assets/f369719d-8e0c-4bb4-968a-c8d5cda327b9" />

- Anonymous FTP was allowed.



<img width="581" height="252" alt="image" src="https://github.com/user-attachments/assets/9df5010f-5a64-4311-b7bc-c46263c9b25b" />

- `task.txt` — contained the small task list and ended with `-lin`(username)


<img width="1919" height="737" alt="image" src="https://github.com/user-attachments/assets/ba61464a-b179-42f5-932e-b4c0756d4277" />

- `locks.txt` — contained many password.

---

## Exploitation

### Hydra
<img width="1919" height="494" alt="image" src="https://github.com/user-attachments/assets/2e54c989-26ab-44da-ae4f-55cc54470097" />

- Hydra found a valid credential:
```bash
lin : RedDr4gonSynd1cat3
```

---

### SSH Login
<img width="1919" height="789" alt="image" src="https://github.com/user-attachments/assets/70a2adfe-4a43-4802-815d-5fdcf83970bd" />

- Login:
```bash
ssh lin@10.10.87.47
password: RedDr4gonSynd1cat3
```

### First Flag
<img width="573" height="86" alt="1" src="https://github.com/user-attachments/assets/34d5fd43-8acc-45d6-af99-01f07932647c" />

- Flag found: `[FLAG FOUND]`

---

## Privilege Escalation

### Sudo Privileges
<img width="1563" height="239" alt="image" src="https://github.com/user-attachments/assets/e5e8009e-7bd5-4416-a860-17ef7d7e9533" />

- This means `lin` can run `/bin/tar` as root via sudo.


### Abusing tar to get root & Second Flag
<img width="875" height="275" alt="image" src="https://github.com/user-attachments/assets/6d488c29-14fc-40c5-8e0a-b82c891278e7" />

- After execution the shell is root:

<img width="1918" height="816" alt="1" src="https://github.com/user-attachments/assets/84b3eb3b-a7e6-483f-a81b-affb57822219" />

- Flag found: `[FLAG FOUND]`
