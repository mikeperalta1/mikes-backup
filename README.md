# Mikes Backup
Easily run both *full* and *differential* backups with rsync, to a local folder or an SSH server.

This script is really just a wrapper around rsync's beautiful functionality. It presents a simplified interface for one very narrow use case: Simplifying the process of running daily backups:
* You may easily force a *full* of *differential* backup type with a simple command line argument (see below)
* Otherwise, it will automatically choose a *full* or *differential* backup type, based on whether it detects an existing *full* backup folder at the backup destination
* For *differential* backups, it automatically generates a folder based on today's date and time, making it easier to store many differentials without the need to manually fuss with anything

## Requirements
* rsync
* python3
* Backup destination accessible as a local directory OR a remote SSH server

## Command Line Arguments
* ```--full``` Forces the script to run a *full* backup
* ```--differential``` Forces the script to run a *differential* backup
* ```--log-dir <directory>``` Let's you set the log output directory
* ```--source-dir <directory>``` Specifies the local source directory
* ```--destination-dir <directory>``` Specifies the backup destination directory
* ```--remote-host <hostname>``` Specifies the remote host, if your backup destination is an SSH server
* ```--remote-user <username>``` Specifies the remote username to use, if your backup destination is an SSH server
* ```--ssh-key <path to key>``` Specifies the local SSH key to use for authentication, if your backup destination is an SSH server
* ```--exclude <dir>``` Specifies a source directory to exclude (can be passed multiple times)

Note that ```--remote-host```, ```--remote-user```, and ```--ssh-key``` are only needed if your backup destination is a remote SSH server. You may omit all three if the destination is a locally mounted folder.

##  Example
For daily use, you'll probably want to create a small bash script that calls this script with the parameters you want, and then call that with cron daily (or whatever your preference is)
```
#!/bin/bash

# Backup to an SSH server
/path/to/mikes-backup \
  --log-dir "/my/log/dir/my-awesome-host-logs/" \
  --source-dir "/home/or/whatever/" \
  --destination-dir "/path/to/backup/destination/" \
  --remote-host "my-awesome-host.home" \
  --remote-user "my-remote-user" \
  --ssh-key "/home/me/.ssh/id_rsa" \
  --exclude "/my/dumb/downloads" \
  --exclude "/my/even/dumber/downloads"

# Backup to a local folder
/path/to/mikes-backup \
  --log-dir "/my/log/dir/local-backups/" \
  --source-dir "/home/or/whatever/" \
  --destination-dir "/local/path/to/backup/destination/" \
  --exclude "/my/dumb/downloads" \
  --exclude "/my/even/dumber/downloads"

```

## Questions
I realize these docs are sparse at best, so please send in questions if you have any, and I will try to update this file or create a Wiki if need be

