---
tags:
  - Enumeration
  - TCP
  - HTTP
  - Tooling
  - HyperTextTransferProtocol
---
We can use it to perform basic HTTP/HTTPS requests (like `GET` and `POST`), parse through HTML pages, download files, authenticate, and even maintain a session with a site. It's very versatile and easy to use in scripting and automation. If you prefer aliases, the Invoke-WebRequest cmdlet is aliased to [[wGet|wGet]], `iwr` and [[cURL]].


#### Get Request with Invoke-WebRequest

```powershell-session
Invoke-WebRequest -Uri "https://web.ics.purdue.edu/~gchopra/class/public/pages/webdesign/05_simple.html" -Method GET | Get-Member
```

#### Filtering Incoming Content

```powershell-session
Invoke-WebRequest -Uri "https://web.ics.purdue.edu/~gchopra/class/public/pages/webdesign/05_simple.html" -Method GET | fl Images
```

#### Raw Content

```powershell-session
Invoke-WebRequest -Uri "https://web.ics.purdue.edu/~gchopra/class/public/pages/webdesign/05_simple.html" -Method GET | fl RawContent
```