---
tags:
  - Recon
  - OpenSourceIntelligence
  - OSINT
---

## Guidance 

Google Dorks can be used to specify the target and gain insight on not commonly viewed pages.

See [[Search Operators]]
### Website Internals

The internal website can be reviewed and have its information extracted:

- Employees 
- Utilised technologies
- Infrastructure 
- Company industry and its ties (e.g. A software design company will probably have a Dev server)

### DNS Lookup 

See [[2. Enumeration/TCP/53. Domain Name System (DNS)/1. Guide#DNS Reverse Lookups/Queries|Guide]]
## Specific Notes

1. Company's main website and the type of business may inform on the type of internal network or the devices on the network. Web server, mobile phones etc
	1. The website's SSL [[CRT (Certificate Files)]] and using [[CRT (Certificate Files)#Search Public CRT Files]]


2.  We can often find the email structure by Googling the domain name, i.e., “@inlanefreight.com” and get some valid emails. From there, we can use a script to scrape various social media sites and mashup potential valid usernames. Some organizations try to obfuscate their usernames to prevent spraying, so they may alias their username like a907 (or something similar) back to `joe.smith`. That way, email messages can get through, but the actual internal username isn’t disclosed, making password spraying harder. Sometimes you can use google dorks to search for `inlanefreight.com filetype:pdf` and find some valid usernames in the PDF properties if they were generated using a graphics editor. From there, you may be able to discern the username structure and potentially write a small script to create many possible combinations and then spray to see if any come back valid.