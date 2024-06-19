
# CMD

```
where /R c:\ *.txt
```

# PowerShell 

Return all files within a path 

```powershell-session
Get-ChildItem -Path C:\Users\MTanaka\ -File -Recurse 
```

Narrow the search for `txt` files

```powershell-session
Get-Childitem –Path C:\Users\MTanaka\ -File -Recurse -ErrorAction SilentlyContinue | where {($_.Name -like "*.txt")}
```

Adding conditionals to the filtering using `where`, see [[Everything is an Object]]

```powershell-session
PS C:\htb> Get-Childitem –Path C:\Users\MTanaka\ -File -Recurse -ErrorAction SilentlyContinue | where {($_.Name -like "*.txt" -or $_.Name -like "*.py" -or $_.Name -like "*.ps1" -or $_.Name -like "*.md" -or $_.Name -like "*.csv")}
```

Search within all found files:

```powershell-session
 Get-ChildItem -Path C:\Users\MTanaka\ -Filter "*.txt" -Recurse -File | Select-String "Password","credential","key"
```

Filter on files:

```
Get-ChildItem -Path "./" -Recurse | where Length -gt 0
```

Combining filtering and searching for strings:

```powershell-session
Get-Childitem –Path C:\Users\MTanaka\ -File -Recurse -ErrorAction SilentlyContinue | where {($_. Name -like "*.txt" -or $_. Name -like "*.py" -or $_. Name -like "*.ps1" -or $_. Name -like "*.md" -or $_. Name -like "*.csv")} | Select-String "Password","credential","key","UserName"
```

## Hidden Files 

```
Get-ChildItem -Hidden
```