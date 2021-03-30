---
published: true
---
**HackTheBox**

Box: **Lame**

IP: **10.10.10.3**

Let's fire off our NMAP scan of **nmap -A -p- -T4 10.10.10.3** and see what we get.

![]({{ site.baseurl }}/images/HTB-Lame-Screenshots/First.png "an image title")

**21/tcp   open  ftp         vsftpd 2.3.4
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.0.20-Debian (workgroup: WORKGROUP)**