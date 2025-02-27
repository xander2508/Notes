---
tags:
  - OperatingSystems
  - Linux
  - StandardInformation
---

There are several different types of system logs on Linux, including:
- Kernel Logs
- System Logs
- Authentication Logs
- Application Logs
- Security Logs

#### Kernel logs

These logs contain information about the system's kernel, including hardware drivers, system calls, and kernel events. They are stored in the `/var/log/kern.log` file.

#### System logs

These logs contain information about system-level events, such as service starts and stops, login attempts, and system reboots. They are stored in the `/var/log/syslog` file.

#### Authentication logs

These logs contain information about user authentication attempts, including successful and failed attempts. They are stored in the `/var/log/auth.log` file. It is important to note that while the `/var/log/syslog` file may contain similar login information, the `/var/log/auth.log` file specifically focuses on user authentication attempts, making it a more valuable resource for identifying potential security threats. Therefore, it is essential for penetration testers to review the logs stored in the `/var/log/auth.log` file to ensure that the system is secure and has not been compromised.

#### Application logs

These logs contain information about the activities of specific applications running on the system. They are often stored in their own files, such as `/var/log/apache2/error.log` for the Apache web server or `/var/log/mysql/error.log` for the MySQL database server.

#### Security logs

These security logs and their events are often recorded in a variety of log files, depending on the specific security application or tool in use. For example, the Fail2ban application records failed login attempts in the `/var/log/fail2ban.log` file, while the UFW firewall records activity in the `/var/log/ufw.log` file. Other security-related events, such as changes to system files or settings, may be recorded in more general system logs such as `/var/log/syslog` or `/var/log/auth.log`.