---
published: false
---

**HackTheBox**

Box: **Nibbles**

IP: **10.10.10.75**

Let's start fire off an nmap scan and see what we get. **sudo nmap -A -p- -T4 10.10.10.75**

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/initial-scan.png "an image title")

Look's like SSH and HTTP are running.

Let's navigate to the website, and clikc on the protepries button and see if there is any hidden code on it. 

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/initial-scan.png "an image title")

Looks like there is a directory called **/nibbleblog/**. Let's navigate to that page.

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/hidden-url.png "an image title")

It looks like the blog software is called nibbles. Let's search nibble in searchsploit and metasploit to see if we get any hits.

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/searchsploit.png "an image title")

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/metasploit-search-exploit.png "an image title")

Let's see some more information about the metasploit exploit by selecting it and typing in **info**.

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/exploit-info.png "an image title")

In order to get this exploit to upload a file, we need to be an authenticated user. Let's try and use DirBuster to find a login page on the website.

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/dirbuster.png "an image title")

We get a hit with the path being **nibbleblog/admin.php**.

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/dirbuster-results.png "an image title")

Let's naviage to the page and see what we get.

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/admin-panel.png "an image title")

Let's try and use cewl to create a wordlist to use against the sign in page.

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/cewl-wordlist.png "an image title")

Fire up BurpSuite and send a test login and send that to repeater and set the payload.

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/burp-suite.png "an image title")

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/intriuder.png "an image title")

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/intruder-options.png "an image title")

Once we get authenticated, look around and you should find the version running. It should work with our exploit.

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/nibble-version.png "an image title")

Go back into metasploit and let's set the options.

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/metasploit.png "an image title")

Run the exploit and we can see that we need to get root.

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/metasploit-complete.png "an image title")

Let's try running **sudo -l** which will do xzy and we will see the file **monitor.sh** can be run root with no password.

Get into the folder and run the command **echo "bash -i" > monitor.sh**, when the file is executed it will give you a root bash shell.

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/echo-bash.png "an image title")

Make sure to make the file executable with **chmod +x monitor.sh**.

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/file-permi.png "an image title")

If everythgin works correctly you should see a root shell!

![]({{ site.baseurl }}/images/HTB-Nibbles-Screenshots/root.png "an image title")
