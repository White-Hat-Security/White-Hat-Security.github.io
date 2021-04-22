---
published: false
---
**HackTheBox**

Box: **Devel**

IP: **10.10.10.5**

Let's fire off a rustscan and see what ports are open on the box.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/rustscan.png "an image title")

Looks like ports 21 (FTP) and 80 (HTTP) are open. Let's go to the webpage and see if there is anything on it.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/website-visit.png "an image title")

Look's like we are dealing is a Windows IIS server.

The let's scan the open ports with nmap and see if we can get the service version running on them.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/nmap-scan.png "an image title")

We can see that the ISS version is 7.5. Make a note of that. 

Since the box is running http let's run a directory scanning agains it using DirBuster.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/dirbuster-settings.png "an image title")

Since it's IIS server, use the file expentsion: asm, asmx, asp, and aspx.

While that's running in the background let's see if we can connect over ftp using username **anonymous** and password of **anonymous**.

If we use the put command we try and upload an image file and see if we view it on the web server. If we can, then we can execute files on the server.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/dirbuster-settings.png "an image title")

I uploaded a file called puppy.jpeg and if we go to 10.10.10.5/puppy.jpeg we can see it shows up (sort of).

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/puppy.png "an image title")

Knowing all of this, we need to create a reverse shell using msfvenom and get a reverse shell. 
