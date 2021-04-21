---
published: true
---
**HackTheBox**

Box: **Blue**

IP: **10.10.10.40**

Let's try using **rustscan** and see what ports are open.

![]({{ site.baseurl }}/images/HTB-Blue-Screenshots/rustscan.png "an image title")

Let's use nmap and see what services are running on the machine.

![]({{ site.baseurl }}/images/HTB-Blue-Screenshots/nmap.png "an image title")

Looks like SMB will be the vector for this box.

Let's try and get the SMB version running by using metasploit: **scanner/smb/smb_version**

![]({{ site.baseurl }}/images/HTB-Blue-Screenshots/smb-version-meta.png "an image title")

Doesn't look like we are able to detect what version us running.

![]({{ site.baseurl }}/images/HTB-Blue-Screenshots/smb-version-scan.png "an image title")

Since it's Windows 7 and is running SMB, let's use metasploit to check if it is vulnerable to EternalBlue.

We will use: **scanner/smb/smb_ms17_010**

It looks vulnerable!

![]({{ site.baseurl }}/images/HTB-Blue-Screenshots/meta-aux-results.png "an image title")

Let's search for ms17-010 in metasploit and see what we get.

![]({{ site.baseurl }}/images/HTB-Blue-Screenshots/meta-check-blue.png "an image title")

Let's see what options we need to set.

![]({{ site.baseurl }}/images/HTB-Blue-Screenshots/meta-blue-options.png "an image title")

Looks like we need set the remote host and remote port and it should work.

We run the exploit and we get a shell.

![]({{ site.baseurl }}/images/HTB-Blue-Screenshots/meta-blue-complete.png "an image title")
