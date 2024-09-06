---
tags:
  - OperatingSystems
  - Windows
  - Tooling
  - Files
  - StandardInformation
---
`Comp` will check each byte within two files looking for differences and then displays where they start. By default, the differences are shown in a decimal format. We can use the `/A` modifier if we want to see the differences in ASCII format. The `/L` modifier can also provide us with the line numbers.

```cmd-session
comp .\file-1.md .\file-2.md

Comparing .\file-1.md and .\file-2.md...
Files compare OK  
```

When FC performs its inspection, it is case-sensitive and cares more than just a byte-for-byte comparison. Below we will use a few files with many more characters and strings to test its functionality.

```cmd-session
fc passwords.txt modded.txt /N
```

The output from FC is much easier to interpret and gives us a bit more clarity about the differences between the files.