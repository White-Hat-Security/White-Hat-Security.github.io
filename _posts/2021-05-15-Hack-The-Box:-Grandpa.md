---
published: false
---

**HackTheBox**

Box: **Grandpa**

IP: **10.10.10.14**

Let run a nmap scan and see what is running on the target.

![]({{ site.baseurl }}/images/HTB-Grandpa-Screenshots/inital-scan.png "an image title")

Looks like HTTP is open, so lets navigate to the machine and see if we see anything.

![]({{ site.baseurl }}/images/HTB-Grandpa-Screenshots/webpage.png "an image title")

Doesn't look like anything. 

Let's run dirbuster and and see if there are any hidden directories. 

![]({{ site.baseurl }}/images/HTB-Grandpa-Screenshots/dirbuster.png "an image title")

While that's running let's look for exploits for Microsoft IIS httpd 6.0.

![]({{ site.baseurl }}/images/HTB-Grandpa-Screenshots/web-search.png "an image title")

![]({{ site.baseurl }}/images/HTB-Grandpa-Screenshots/exploit-page-view.png "an image title")

Let's see what the options are in metasploit.

![]({{ site.baseurl }}/images/HTB-Grandpa-Screenshots/exploit-options.png "an image title")

Run the exolpit and we get a shell!

![]({{ site.baseurl }}/images/HTB-Grandpa-Screenshots/exploit-success.png "an image title")

If we run some commands we see that we are not NT Authority.

![]({{ site.baseurl }}/images/HTB-Grandpa-Screenshots/inital-meta-look.png "an image title")

Let's see what processes are running on the machine using **ps**.

![]({{ site.baseurl }}/images/HTB-Grandpa-Screenshots/services-migrate.png "an image title")

We see three of them are running as NT Authority\Network Service, let;s try and migrate our current session to get more permissions on the system.

![]({{ site.baseurl }}/images/HTB-Grandpa-Screenshots/get-system.png "an image title")

Nex, let's background the sessions and use the exploit_suggester to get NT Authority\System.

![]({{ site.baseurl }}/images/HTB-Grandpa-Screenshots/priv-suggester.png "an image title")

Run the suggester and we see a list of possible exploits.

![]({{ site.baseurl }}/images/HTB-Grandpa-Screenshots/suggesters-found.png "an image title")

Let's try the first one ms10_015_kitrap0d.

Let's see the exploit options.

![]({{ site.baseurl }}/images/HTB-Grandpa-Screenshots/firs-exploit.png "an image title")

Run the exploit and we will get NT Authority\System.

![]({{ site.baseurl }}/images/HTB-Grandpa-Screenshots/exploit-works.png "an image title")








