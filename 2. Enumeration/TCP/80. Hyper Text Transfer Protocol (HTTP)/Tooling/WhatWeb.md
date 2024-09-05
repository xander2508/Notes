---
tags:
  - Enumeration
  - TCP
  - HTTP
  - Tooling
  - HyperTextTransferProtocol
---

[GitHub - urbanadventurer/WhatWeb: Next generation web scanner](https://github.com/urbanadventurer/WhatWeb)

WhatWeb identifies websites. Its goal is to answer the question, "What is that Website?". WhatWeb recognises web technologies including content management systems (CMS), blogging platforms, statistic/analytics packages, JavaScript libraries, web servers, and embedded devices. WhatWeb has over 1800 plugins, each to recognise something different. WhatWeb also identifies version numbers, email addresses, account IDs, web framework modules, SQL errors, and more.

```
./whatweb reddit.com

http://reddit.com [301 Moved Permanently] Country[UNITED STATES][US], HTTPServer[snooserv], IP[151.101.65.140], RedirectLocation[https://www.reddit.com/], UncommonHeaders[retry-after,x-served-by,x-cache-hits,x-timer], Via-Proxy[1.1 varnish]
https://www.reddit.com/ [200 OK] Cookies[edgebucket,eu_cookie_v2,loid,rabt,rseor3,session_tracker,token], Country[UNITED STATES][US], Email[banner@2x.png,snoo-home@2x.png], Frame, HTML5, HTTPServer[snooserv], HttpOnly[token], IP[151.101.37.140], Open-Graph-Protocol[website], Script[text/javascript], Strict-Transport-Security[max-age=15552000; includeSubDomains; preload], Title[reddit: the front page of the internet], UncommonHeaders[fastly-restarts,x-served-by,x-cache-hits,x-timer], Via-Proxy[1.1 varnish], X-Frame-Options[SAMEORIGIN]
```

## Installation

[Releases · urbanadventurer/WhatWeb](https://github.com/urbanadventurer/WhatWeb/releases)

```
unzip WhatWeb-v0.5.2.zip
```
```
cd WhatWeb-0.5.2/
```
### Search Plugins

To view more detail about a plugin or search plugins for a keyword:

```
$ ./whatweb -I phpBB
```