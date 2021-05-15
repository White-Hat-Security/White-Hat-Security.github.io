---
published: false
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









