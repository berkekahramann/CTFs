## Bilgi
- Platform: TryHackMe  
- Zorluk: Easy

---

## Enumeration

### Nmap
```bash
nmap -sV -O 10.10.53.170
```
<img width="1919" height="834" alt="image" src="https://github.com/user-attachments/assets/940a7c99-59f3-41bb-909e-b017ebab1b9f" />
<pre>Açık portlar: 
22/tcp → SSH (OpenSSH 8.2p1) 
80/tcp → HTTP (Apache 2.4.41) 
</pre>

### Web İnceleme
#### Anasayfa
