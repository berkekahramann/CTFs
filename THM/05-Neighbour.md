## Info
- Platform: TryHackMe  

---

## Enumeration
<img width="1919" height="831" alt="image" src="https://github.com/user-attachments/assets/3371018c-add3-487d-a97f-acb9cd02bfd7" />

- Login page discovered at `http://10.10.93.62`.  

<img width="1919" height="765" alt="image" src="https://github.com/user-attachments/assets/b125aacf-1632-4639-a5e9-09d4789ddc8b" />

- Source code analyzed.  
- Guest credentials (`guest:guest`) identified in HTML comments.  

---

## Exploitation
<img width="1918" height="834" alt="image" src="https://github.com/user-attachments/assets/c6c50942-f5d2-429c-8006-0ebe43c85257" />

- Login performed with `guest:guest`.  
- User profile accessed at `/profile.php?user=guest`.  
- Parameter changed from `guest` to `admin`.  

---

## Result
<img width="1913" height="830" alt="image" src="https://github.com/user-attachments/assets/e0acb7bb-f434-4102-b7fb-4e73034b35f7" />

- Flag found: `[FLAG FOUND]`
