
The [[1. Recon/Port Scanning/Nmap/1. Overview]] XML output, can easily create HTML reports that are easy to read, even for non-technical people. This is later very useful for documentation, as it presents our results in a detailed and clear way. To convert the stored results from XML format to HTML, we can use the tool `xsltproc`.

More information about the output formats can be found at: [https://nmap.org/book/output.html](https://nmap.org/book/output.html)

```
xsltproc ./scan.xml > scan.html
```