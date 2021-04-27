---
published: false
---
**HackTheBox**

Box: **Devel**

IP: **10.10.10.95**

Let's start an nmap scan and see what ports are open on the box. 

![]({{ site.baseurl }}/images/HTB-Jerry-Screenshots/initial-scan.png "an image title")

We can see that port 8080 (HTTP) is open and is running a **Tomcat 7.0.88** web server. Let's go and see what the webpage looks like. 

![]({{ site.baseurl }}/images/HTB-Devel-Screenshots/look-at-webpage.png "an image title")

We see the version of tomcat running again. If we click on the Manager App button on the right we are promptedt with a login window.

![]({{ site.baseurl }}/images/HTB-Jerry-Screenshots/login-screen.png "an image title")

Run BurpSuite and then let's send some credentials and see what shows up in BurpSuite. I entered in test:test.

![]({{ site.baseurl }}/images/HTB-Jerry-Screenshots/data-for-burp.png "an image title")

In BurpSuite, under the proxy tab, under HTTP history tab, we should see the get request we sent with the practice credentials. They are encoded in base64

![]({{ site.baseurl }}/images/HTB-Jerry-Screenshots/login-screen.png "an image title")

Highlight the base64 string, righ-click and hit send to Decoder.

![]({{ site.baseurl }}/images/HTB-Jerry-Screenshots/right-click-send.png "an image title")

Click the Decoder tab and then select the type of decoder string on the right.

![]({{ site.baseurl }}/images/HTB-Jerry-Screenshots/base64-decode.png "an image title")

You should then see the decoded text appear at the bottom of the screen.

![]({{ site.baseurl }}/images/HTB-Jerry-Screenshots/base64-results.png "an image title")

Since the web server is running Tomcat, let's search on the interent for the default credneitlas and try using them agains the site. Thi github page has them.

![]({{ site.baseurl }}/images/HTB-Jerry-Screenshots/tomcat-default-creds.png "an image title")

Copy and paste the credentials into a word doc and then use the find and replace option to replace the space with a colon (:).

![]({{ site.baseurl }}/images/HTB-Jerry-Screenshots/paste-default-creds.png "an image title")

Next I am going to go to a base64 website converter and paste in the formatted credentials, and then encode them.

![]({{ site.baseurl }}/images/HTB-Jerry-Screenshots/base64-site-url.png "an image title")

![]({{ site.baseurl }}/images/HTB-Jerry-Screenshots/base64-site.png "an image title")

Back in burp suite, right click a GET request and then click Send to Repeater. 

![]({{ site.baseurl }}/images/HTB-Jerry-Screenshots/burp-send-to-reapeater.png "an image title")

Click on the Intruder tab and then hit the Clear button on the right and then highlight the base64 text and hit the Add button. 
![]({{ site.baseurl }}/images/HTB-Jerry-Screenshots/intruder-options.png "an image title")