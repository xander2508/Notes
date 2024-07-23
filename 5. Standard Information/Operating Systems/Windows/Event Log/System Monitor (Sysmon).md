- Real-time monitoring of system activities
- Detailed process and network connection tracking
- Advanced threat detection capabilities
- Centralized logging and reporting functionality
- Integration with SIEM solutions for enhanced security analysis
- A device driver that assists in capturing the system activity data.
- An event log to display captured activity data.

`System Monitor (Sysmon)` is a Windows system service and device driver that remains resident across system reboots to monitor and log system activity to the Windows event log. Sysmon provides detailed information about process creation, network connections, changes to file creation time, and more.

Sysmon's unique capability lies in its ability to log information that typically doesn't appear in the Security Event logs, and this makes it a powerful tool for deep system monitoring and cybersecurity forensic analysis.

Sysmon Event IDs: [Sysmon - Sysinternals | Microsoft Learn](https://learn.microsoft.com/en-us/sysinternals/downloads/[[System Monitor (Sysmon)

Sysmon uses an XML-based configuration file:
* For a comprehensive configuration, we can visit: [https://github.com/SwiftOnSecurity/sysmon-config](https://github.com/SwiftOnSecurity/sysmon-config)
* 