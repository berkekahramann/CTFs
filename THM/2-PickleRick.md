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
