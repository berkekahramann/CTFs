## Bilgi
- Platform: TryHackMe  
- Zorluk: Easy

---

## Enumeration

### Nmap
```bash
nmap -sV -O 10.10.53.170
```

<pre>Açık portlar: 
22/tcp → SSH (OpenSSH 8.2p1) 
80/tcp → HTTP (Apache 2.4.41) 
</pre>

### Web İnceleme
#### Anasayfa
