If requests to pages or parameters changes based on what is sent, maybe there is a WAF blocking certain requests. Attempt to send " " or "", then "echo" etc

1. Burp can bypass WAF, see [[Burp#WAF Bypass]]
2. Get the server to make the requests on your behalf
	* [[XML#XML External Entity XXE Injection]]
	* [[Command Line Restrictions#Bypass Through Escalation]]
1. Vary the data sent to the parameter or page using blank spaces e.g. `/sync?opt=' pw''d'"`, see [HTB: FluxCapacitor | 0xdf hacks stuff](https://0xdf.gitlab.io/2018/05/12/htb-fluxcapacitor.html)
2. Bash restrictions may be applying which restrict the commands to run, see [[Command Line Restrictions]]
