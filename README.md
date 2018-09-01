# Mikes Backup
A simple python script utilizing rsync for both full and differential backups, and auto folder naming, over SSH

Honestly this is more of a wrapper around rsync's beautiful functionality. It simply makes daily backups slightly easier by:
* Automatically choosing a *full* or *differential* backup type, based on whether it detects an existing *full* backup folder at the remote end
* Automatically generate a folder based on today's date and time, so you can generate a great many *differential* backup folders without manually changing anything

## Requirements
* rsync
* python3
* Backup server accessible over SSH

## Assumptions
* Your backup destination is an SSH server

## Command Line Arguments
* ```--full``` Forces the script to run a *full* backup
* ```--differential``` Forces the script to run a *differential* backup
* ```--log-dir <directory>``` Let's you set the log output directory
* ```--source-dir <directory>``` Specifies the local source directory
* ```--remote-host <hostname>``` Specifies the remote host, to send the backups to over ssh
* ```--remote-user <username>``` Specifies the remote username to use, when connecting to the remote host
* ```--remote-dir <directory>``` Specifies the remote backup destination directory
* ```--ssh-key <path to key>``` Specifies the local ssh key to use for authentication
* ```--exclude <dir>``` Specifies a source directory to exclude (can be passed multiple times)

##  Example
For daily use, you'll probably want to create a small bash script that calls this script with the parameters you want, and then call that with cron daily (or whatever your preference is)
```#!/bin/bash

/path/to/mikes-backup --log-dir "/my/log/dir" --source-dir "/home/or/whatever" --remote-host "my-awesome-host.home" --remote-user "me" --remote-dir "/path/to/backup/destination/on/remote/" --ssh-key "/home/me/.ssh/id_rsa" --exclude "/my/dumb/downloads"```

## Questions
I realize these docs are sparse at best, so please send in questions if you have any, and I will try to update this file or create a Wiki if need be

