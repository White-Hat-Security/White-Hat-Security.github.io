---
published: true
---
**HackTheBox**

Box: **Lame**

IP: **10.10.10.3**

Let's fire off our NMAP scan of **nmap -A -p- -T4 10.10.10.3** and see what we get.

![]({{ site.baseurl }}/images/HTB-Lame-Screenshots/First.png "an image title")

We can see a couple of different services running.

Since we get the Samba version (**Samba smbd 3.0.20-Debian**) right away  let's see what exploits there are for it out on the web.

By searching **smbd 3.0.20-Debian exploit** we can see Rapid7's website pops up.

Open up the site.

![]({{ site.baseurl }}/images/HTB-Lame-Screenshots/possible exploit.png "an image title")

And we can see that this exploit effect version 3.0.20 through 3.0.25rc3.

The nice thing about Rapid7 that they can have the exploit location for metasploit typed out for you.

![]({{ site.baseurl }}/images/HTB-Lame-Screenshots/possible exploit.png "an image title")

Let's fire up metasploit and see what option we get for the exploit.

![]({{ site.baseurl }}/images/HTB-Lame-Screenshots/exploit example.png "an image title")

Looks like we just need to set the remote host and the local host.

If we run the exploit we get a shell!

![]({{ site.baseurl }}/images/HTB-Lame-Screenshots/connection.png "an image title")

We have successfuly rooted this machine! Thanks for reading!