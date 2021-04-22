---
published: true
---
**HackTheBox**

Box: **Devel**

IP: **10.10.10.5**

Let's fire off a rustscan and see what ports are open on the box.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/rustscan.png "an image title")

Looks like ports 21 (FTP) and 80 (HTTP) are open. Let's go to the web page and see if there is anything on it.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/website-visit.png "an image title")

Look's like we are dealing is a Windows IIS server.

The let's scan the open ports with nmap and see if we can get the service version running on them.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/nmap-scan.png "an image title")

We can see that the ISS version is 7.5. Make a note of that. 

Since the box is running HTTP let's run a directory scanning against it using DirBuster.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/dirbuster-settings.png "an image title")

Since it's IIS server, use the file extension: asm, asmx, asp, and aspx.

While that's running in the background let's see if we can connect over ftp using username **anonymous** and password of **anonymous**.

If we use the put command we try and upload an image file and see if we view it on the web server. If we can, then we can execute files on the server.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/dirbuster-settings.png "an image title")

I uploaded a file called puppy.jpeg and if we go to 10.10.10.5/puppy.jpeg we can see it shows up (sort of).

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/puppy.png "an image title")

It looks like we should be able to create a payload in msfvenom and execute on the IIS server.

This msfvenom cheat sheet should help us configure the right kind of payload. 

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/msfvenom-website.png "an image title")

Let's use the ASPX one (not the asp as shown).

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/msfvenom-site-payload.png "an image title")

Copy and paste the command in the terminal and add your IP and the port you want to listen on and hit enter.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/msfvenom-command.png "an image title")

Next let's ftp back into the target and upload the file.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/put-the-code.png "an image title")

After that let's run metasploit and run the handler module to be able to revice back the connection from the payload we just put onto the target. 

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/meta-exploit handler.png "an image title")

Let's see what options we get for the handler.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/meta-options.png "an image title")

Let's set the IP and ports and also let's set the payload to be **meterpreter_reverse_tcp**

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/set-correct-payload.png "an image title")

Next let's go to the webpage to run the code. For me it was **10.10.10.5/shell.aspx**.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/aspx-white-screen.png "an image title")

Run the metasploit listener and you should a shell.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/got-shell.png "an image title")

If we run **getuid** we can see that we are not root and if we try running the **getsystem** command it doesn't work. 

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/not-root "an image title")

Let's use the exploit suggester in metasploit and see what exploits it finds.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/search-suggester.png "an image title")

If we look at the options we see that we only need to set the session number.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/suggester-opttions.png "an image title")

We run the suggester and see a list fo exploits that metasploit thinks it can use against the target.

Let's try the first one on the list: **ms10_015**

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/exploit-suggester-results.png "an image title")

Let's select the exploit and see what options we need to configure.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/new-expl oit-settings.png "an image title")

Looks like just the session id and our IP address.

We run the exploit, get a shell, and if we run the command **getuid** we see that we have successfully rooted this machine.

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/no-sessions.png "an image title")

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/exploit-to-get-root.png "an image title")