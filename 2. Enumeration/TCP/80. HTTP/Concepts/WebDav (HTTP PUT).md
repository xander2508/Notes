Web Distributed Authoring and Versioning (WebDAV) is an HTTP extension designed to allow people to create and modify web sites using HTTP. It was originally started in 1996, when this didn’t seem like a terrible idea.
# Guide
1. [HTB: Granny | 0xdf hacks stuff](https://0xdf.gitlab.io/2019/03/06/htb-granny.html)
2. [Command-line utility for WebDAV upload - Stack Overflow](https://stackoverflow.com/questions/1205101/command-line-utility-for-webdav-upload)

```
curl -T filetoput.xml http://www.url.com/filetoput.xml
```


# Tooling

`davtest`

```
davtest -url http://10.10.10.15
```