---
published: true
---
**HackTheBox**

Box: **Bashed**

IP: **10.10.10.68**

Let's run our nmap scan and see what we get.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/initial-scan.png "an image title")

It looks like another HTTP box.

Let's navigate to the webpage and see what we get.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/web-page.png "an image title")

If we click around we see a screen that chnages and on it we see a path to **/uploads/phpbash.php**.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/uploads-folder-location.png "an image title")

If you navigate to the it, nothing of interest appears.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/blank-uploads.png "an image title")

Next, let's fire up DirBuster and see if we can find some more directories.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/dirbuster.png "an image title")

A direcotry that looks interesting is **/dev/phpbash.php**.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/location.png "an image title")

If we navigate to the directory we see we get a some sort of webpage shell.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/found-terminal.png "an image title")

Let's try running the command **sudo -l** to see what can be run without passwords.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/sudo-l.png "an image title")

Look's like the user **scriptmanager** can be switched to without needing a passwords. Let's try that.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/try-switch-user.png "an image title")

Look's like we need to get **tty** to be able to switch into the user.

Let's see if we can use wget to uploads files.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/wget-works.png "an image title")

Look's like it works.

Next let's google for php reverse shells. This github will have what we need.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/github-reverse-shell.png "an image title")

Let's clone the repo.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/git-reverse-shell.png "an image title")

Next, let's get into the file and chnaged the **ip** and **port** to talk back to our machine.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/stuff-to-change.png "an image title")

Next, let's spin up a python web server to host the shell.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/host-file.png "an image title")

And then from the webshell, lets use wget and grab the file from our host machine.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/grab-the-shell.png "an image title")

In order to execute the reverse shell, we need to navigaet to the path it is at. **10.10.10.68/uploads/php-reverse-shell.php**

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/site-execute.png "an image title")

Next, let's listen on port 4444 using **nc -nvlp 4444** and if everything works, we should get a connection.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/netcat.png "an image title")

In order to get TTY, let's google spawning tty lines in python.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/tty-site.png "an image title")

Let's start at the top of the list, and paste into our nc connection this python command. **python -c 'import pty; pty.spawn("/bin/sh")'**

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/tty-site-loaded.png "an image title")

And we should, finally, get a proper shell.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/get-shell.png "an image title")

Let's try switching into the scriptmanager account using **sudo su scriptmanager**.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/fail-su.png "an image title")

That didn't work, lets try using **sudo -u scriptmanager /bin/bash**. The -u flag will run the command as the speicfied user. In this case it will tell linux to open a bash shell as scriptmanager.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/run-as-user.png "an image title")

As this user let's see what folders he has access to using **ls -altr**.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/interesting-folder.png "an image title")

We see a folder called **scripts** that the user has full rights to. Navigate to the folder and we see two files and the py is a script that runs like every minutes, which opens and then writes to a file called test.txt.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/pytohn-file.png "an image title")

Let's google for a python reverse shell to execute in that script. Pentestmonkey has one we will use.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/python-reverse-shell.png "an image title")

Copy and paste the code into a new file and set the IP and port to our machine. (make sure you call the file test.py)

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/python-reverse-shamges.png "an image title")

Next, fire up another netcat listener. Make sure it listens on the ports of the python reverse shell.

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/another-listener.png "an image title")

Next, spin up a python web server to host the reversre shell to get it onto the target machine. 

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/wget-python.png "an image title")

If everything works correctly, you should get a connection and then run the command **python -c 'import pty; pty.spawn("/bin/sh")'** to get a bash shell as root!

![]({{ site.baseurl }}/images/HTB-Bashed-Screenshots/root.png "an image title")





