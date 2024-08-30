---
tags:
  - OperatingSystems
  - Linux
  - Tooling
  - BackupAndRestore
---
Rsync is an open-source tool that allows us to quickly and securely back up files and folders to a remote location. It is particularly useful for transferring large amounts of data over the network, as it only transmits the changed parts of a file. It can also be used to create backups locally or on remote servers. If we need to back up large amounts of data over the network, Rsync might be the better option.


This command will copy the entire directory (`/path/to/mydirectory`) to a remote host (`backup_server`), to the directory `/path/to/backup/directory`. The option `archive` (`-a`) is used to preserve the original file attributes, such as permissions, timestamps, etc., and using the `verbose` (`-v`) option provides a detailed output of the progress of the `rsync` operation.

```shell-session
rsync -av /path/to/mydirectory user@backup_server:/path/to/backup/directory
```


We can also add additional options to customize the backup process, such as using compression and incremental backups. We can do this like the following:

```shell-session
rsync -avz --backup --backup-dir=/path/to/backup/folder --delete /path/to/mydirectory user@backup_server:/path/to/backup/directory
```

With this, we back up the `mydirectory` to the remote `backup_server`, preserving the original file attributes, timestamps, and permissions, and enabled compression (`-z`) for faster transfers. The `--backup` option creates incremental backups in the directory `/path/to/backup/folder`, and the `--delete` option removes files from the remote host that is no longer present in the source directory.

If we want to restore our directory from our backup server to our local directory, we can use the following command:

```shell-session
rsync -av user@remote_host:/path/to/backup/directory /path/to/mydirectory
```


# Secure Transfer of our Backup

To ensure the security of our `rsync` file transfer between our local host and our backup server, we can combine the use of SSH and other security measures.

```shell-session
rsync -avz -e ssh /path/to/mydirectory user@backup_server:/path/to/backup/directory
```


## Auto-Synchronization

To enable auto-synchronization using `rsync`, you can use a combination of `cron` and `rsync` to automate the synchronization process. Scheduling the cron job to run at regular intervals ensures that the contents of the two systems are kept in sync.

Therefore we create a new script called `RSYNC_Backup.sh`, which will trigger the `rsync` command to sync our local directory with the remote one.

```bash
#!/bin/bash

rsync -avz -e ssh /path/to/mydirectory user@backup_server:/path/to/backup/directory
```

```shell-session
chmod +x RSYNC_Backup.sh
```

```shell-session
0 * * * * /path/to/RSYNC_Backup.sh
```