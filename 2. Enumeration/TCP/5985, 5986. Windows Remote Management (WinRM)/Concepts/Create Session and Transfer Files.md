---
tags:
  - Post-Exploitation
  - DataTransfer
  - Windows
---

In the example below, a session is created to the remote computer named `DATABASE01` and stores the results in the variable named `$Session`.

```powershell-session
$Session = New-PSSession -ComputerName DATABASE01
```

We can use the `Copy-Item` cmdlet to copy a file from our local machine `DC01` to the `DATABASE01` session we have `$Session` or vice versa.

#### Copy samplefile.txt from our Localhost to the DATABASE01 Session

```powershell-session
Copy-Item -Path C:\samplefile.txt -ToSession $Session -Destination C:\Users\Administrator\Desktop\
```

#### Copy DATABASE.txt from DATABASE01 Session to our Localhost

```powershell-session
Copy-Item -Path "C:\Users\Administrator\Desktop\DATABASE.txt" -Destination C:\ -FromSession $Session
```