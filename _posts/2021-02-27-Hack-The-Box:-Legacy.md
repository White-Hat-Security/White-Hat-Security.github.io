---
published: true
---
**HackTheBox**

Box: **Legacy**

IP: **10.10.10.4**

For all of these walkthroughs, I used [pimpmykali](https://github.com/Dewalt-arch/pimpmykali) on my Kali VM.

![]({{ site.baseurl }}/images/HTB-Legacy-Screenshots/first.png "an image title")

For all of these walkthroughs, I used [pimpmykali](https://github.com/Dewalt-arch/pimpmykali) on my Kali VM.

Let's fire up an nmap scan and see what we have to work with.

**sudo nmap -T4 -A -p- 10.10.10.4**

![]({{ site.baseurl }}/images/HTB-Legacy-Screenshots/first.png "an image title")

Looks like ports 139, 445, and 3389 are open. Let's go after SMB first. 
(If you need a quick port number cheat sheet, this [list](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers) from wikipedia is quite good.)

Let's do some enumeration of SMB with enum4linux with the -n switch and see what we get.

![]({{ site.baseurl }}/images/HTB-Legacy-Screenshots/third.png "an image title")

We can see what shares are available and that blank username and passwords can be used to authentic to SMB.  

We still don't have the version, so let's fire up metasploit and see if we can get it. If we search metasploit for a SMB scanner we find smb_version.

![]({{ site.baseurl }}/images/HTB-Legacy-Screenshots/fourth.png "an image title")

Let's select it and see the options.

![]({{ site.baseurl }}/images/HTB-Legacy-Screenshots/fith.png "an image title")

Looks like we just need to set the remote host (RHOST) and run it.

![]({{ site.baseurl }}/images/HTB-Legacy-Screenshots/fith.png "an image title")

After running it we still don't get the SMB version, but we do get the OS version: Windows XP SP3 and we can use this to locate an exploit for the machine.

![]({{ site.baseurl }}/images/HTB-Legacy-Screenshots/six.png "an image title")

Searching for Windows XP SP3 exploit shows that the machine might be vulnerable to MS08-067.

![]({{ site.baseurl }}/images/HTB-Legacy-Screenshots/eith.png "an image title")

If we search for ms08_067 in metasploit we can see that it already has a built in module. 

![]({{ site.baseurl }}/images/HTB-Legacy-Screenshots/nineth.png "an image title")

Let's select it and see what option are availalbe.

![]({{ site.baseurl }}/images/HTB-Legacy-Screenshots/tenth.png "an image title")

Look's like all we need to set is the remote host at 10.10.10.4.

If we run the exploit we get a meterpreter session!

![]({{ site.baseurl }}/images/HTB-Legacy-Screenshots/twelth.png "an image title")

Thanks for reading!