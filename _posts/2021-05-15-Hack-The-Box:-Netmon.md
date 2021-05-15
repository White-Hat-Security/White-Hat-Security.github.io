---
published: true
---
**HackTheBox**

Box: **Netmon**

IP: **10.10.10.152**

Let's run our nmap scan and see what the target is running.

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/initial-scan.png "an image title")

Since port 80 is open let's go to the machine and see what webpage is on it.

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/webpage-visit.png "an image title")

looks like a login screen.

Next let's see if we can get anonymous ftp access.

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/ftp-login.png "an image title")

And we can.

Let's look for default credentials for PRTG Network Monitor.

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/default-creds.png "an image title")

If we try them we see it doesn't work.

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/failed-creds.png "an image title")

Since we have access to the machine through ftp let's google how the software stores its passwords and maybe we can find them.

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/find-creds.png "an image title")

Looks like it stores them in this file.

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/database-location.png "an image title")

Back in FTP let's get into the folder.

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/ftp-cd.png "an image title")

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/cd-bypass.png "an image title")

We can then see three dat files, let's download them and look at them.

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/database-files.png "an image title")

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/ftp-download.png "an image title")

Open the latest file in any text editor and if we search for password we get an hashed password.

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/encrypted-password.png "an image title")

Same in the older file.

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/also-encrypt.png "an image title")

In the oldest file, we find the username and password not hashed.

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/found-creds.png "an image title")

If we try the creds ew found it doesnt work, but if we increment the last number by 1, the creds will work!

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/password-incre.png "an image title")

We succesffuly get access to the software.

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/login-success.png "an image title")

Get the version of the PRTG software and we see that it is vulenrable to a remote code authentication exploit. 

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/download-exploit.png "an image title")

In order to run the exploit we will need our auth cookies. We can get those in firefox by right-clicking and slecting inspect elemt and then going to the storage tab and clicking on the OCTOPUS cookie. Copy it.

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/auth-cookie.png "an image title")

Download the exploit and set it up. (I had to fix the script with this sed command: **sed -i -e 's/\r$//' script.sh**)

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/prtg-exploit.png "an image title")

A username and password will then created on the target.

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/exploit-success.png "an image title")

If we then use psexec.py (from [impacket](https://github.com/SecureAuthCorp/impacket)) and our newly created account, we can access the machine as root!

![]({{ site.baseurl }}/images/HTB-Netmon-Screenshots/final.png "an image title")
