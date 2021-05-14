---
published: false
---
**HackTheBox**

Box: **Jerry**

IP: **10.10.10.8**


Let's run our nmap scan and see what we get. **sudo nmap -A -p- -T4 10.10.10.8**

![]({{ site.baseurl }}/images/HTB-Optimum-Screenshots/initial-scan.png "an image title")

Looks like it's another box with HTTP and some software called HFS 2.3, so let's navigate to it's webpage.

![]({{ site.baseurl }}/images/HTB-Optimum-Screenshots/webpage.png "an image title")

We don't see anythin, but let's search for exploits for HttpFileServer (HFS) 2.3. Looks like rapid7 has a post.

![]({{ site.baseurl }}/images/HTB-Optimum-Screenshots/search.png "an image title")

And it works on HFS 2.3b.

![]({{ site.baseurl }}/images/HTB-Optimum-Screenshots/rapid7.png "an image title")

Scroll down and you will see the metasploit syntax needed.

![]({{ site.baseurl }}/images/HTB-Optimum-Screenshots/module-options.png "an image title")

Fire up metasploit and set the options and execute.

![]({{ site.baseurl }}/images/HTB-Optimum-Screenshots/metasploit.png "an image title")

![]({{ site.baseurl }}/images/HTB-Optimum-Screenshots/exploit.png "an image title")

We see that we are not root, and are unable to get root using **getsystem**. Let's background our network connection session and use the suggester tool to see if metasploit can find and exploits it thinks will work against the target.

![]({{ site.baseurl }}/images/HTB-Optimum-Screenshots/exploit-suggester.png "an image title")

Select suggester, the only thing that needs to be set is the session number.

![]({{ site.baseurl }}/images/HTB-Optimum-Screenshots/suggester-options.png "an image title")

get pic of suggester options and executing against it.


maybe have other stuff as different post




