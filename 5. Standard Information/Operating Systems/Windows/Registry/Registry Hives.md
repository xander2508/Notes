---
tags:
  - OperatingSystems
  - Windows
  - Registry
  - StandardInformation
---
Each Windows host has a set of predefined Registry keys that maintain the host and settings required for use. Below is a breakdown of each hive and what can be found referenced within.

| **Name**            | **Abbreviation** | **Description**                                                                                                                                                                                                                                                                                                        |
| ------------------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| HKEY_LOCAL_MACHINE  | `HKLM`           | This subtree contains information about the computer's `physical state`, such as hardware and operating system data, bus types, memory, device drivers, and more.                                                                                                                                                      |
| HKEY_CURRENT_CONFIG | `HKCC`           | This section contains records for the host's `current hardware profile`. (shows the variance between current and default setups) Think of this as a redirection of the [HKLM](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc739525(v=ws.10)) CurrentControlSet profile key. |
| HKEY_CLASSES_ROOT   | `HKCR`           | Filetype information, UI extensions, and backward compatibility settings are defined here.                                                                                                                                                                                                                             |
| HKEY_CURRENT_USER   | `HKCU`           | Value entries here define the specific OS and software settings for each specific user. `Roaming profile` settings, including user preferences, are stored under HKCU.                                                                                                                                                 |
| HKEY_USERS          | `HKU`            | The `default` User profile and current user configuration settings for the local computer are defined under HKU.                                                                                                                                                                                                       |
There are other predefined keys for the Registry, but they are specific to certain versions and regional settings in Windows. For more information on those entries and Registry keys in general, check out the documentation provided by [Microsoft](https://learn.microsoft.com/en-us/windows/win32/sysinfo/predefined-keys)