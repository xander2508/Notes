---
tags:
  - OperatingSystems
  - Windows
  - Tooling
  - Files
  - StandardInformation
---

# CMD
## Find 


```cmd-session
find /i "see" < test.txt
```

```cmd-session
find "password" "C:\Users\student\not-passwords.txt" 
```

The `/V` modifier can change our search from a matching clause to a `Not` clause. So, for example, if we use `/V` with the search string password against a file, it will show us any line that does not have the specified string. 

We can also use the `/N` switch to display line numbers for us and the `/I` display to ignore case sensitivity.

## FindStr

The `findstr` command is similar to `find` in that it searches through files but for patterns instead. It will look for anything matching a pattern, regex value, wildcards, and more. Think of it as find2.0. For those familiar with Linux, `findstr` is closer to `grep`.


# PowerShell


# Select-String

[Select-String](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/select-string?view=powershell-7.2)

 It performs evaluations of input strings, file contents, and more based on regular expression (`regex`) pattern matching. When a match is found, `Select-String` will output the matching `line`, the `name` of the file, and the `line number` on which it was found by default.

An example can be seen in [[Finding Files#PowerShell]]