---
tags:
  - OperatingSystems
  - Windows
  - Tooling
  - Files
---
With `Sort`, we can receive input from the console, pipeline, or a file, sort it and send the results to the console or into a file or another command. It is relatively simple to use and often will be used in conjunction with pipeline operators such as `|`, `<`, and `>`. We can give it a try now by feeding the contents of the `file` file to sort.

```cmd-session
C:\Users\student\Desktop> type .\file-1.md
a
b
d
h
w
a
q
h
g

C:\Users\MTanaka\Desktop> sort.exe .\file-1.md /O .\sort-1.md
C:\Users\MTanaka\Desktop> type .\sort-1.md

a
a
b
d
g
h
h
q
w
```


To sort unique entries:

```cmd-session
sort.exe .\sort-1.md /unique
```