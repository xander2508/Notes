---
tags:
  - OperatingSystems
  - Linux
  - Tooling
  - BackupAndRestore
---
[Rsync](https://linux.die.net/man/1/rsync) is a fast and efficient tool for locally and remotely copying files. It can be used to copy files locally on a given machine and to/from remote hosts. It is highly versatile and well-known for its delta-transfer algorithm. This algorithm reduces the amount of data transmitted over the network when a version of the file already exists on the destination host. It does this by sending only the differences between the source files and the older version of the files that reside on the destination server. It is often used for backups and mirroring. It finds files that need to be transferred by looking at files that have changed in size or the last modified time. By default, it uses port `873` and can be configured to use SSH for secure file transfers by piggybacking on top of an established SSH server connection.

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
