---
дата создания: 2023-02-10 23:06
дата изменений: пятница 10-го февраля 2023 23:06:48
---
# AL-SULTAN SHELL - BOOT SERVICE EXECUTOR

## About

This Folder Is Read By `SHELL BOOT EXECUTOR` For Running All Scripts On It Upon Android System Restart.

## How?

When Android Device Is Restarted The Shell Boot Service Starts And Scan For All Files On Path `~/.boot`. And Start Running Those Scripts On A Separate Job Schedule.

## Instructions

Put Your Script Under Path `~/.boot` And Shell Will Run It When System Restarts. Please Note That SubFolders Will Not Be Scanned, So Put Your Script On Top Folder. Also Note That Scripts Are Scheduled To Run Based On Script Name. i.e. Alphabetically.

## Sample

Simply; To Start `http server` After System Restarts, Create A File Named For Example `run-httpd.sh` On The Folder `~/.boot` With The Below Content:

```sh
#!/data/data/alsultan.shell/rootfs/usr/bin/sh
httpd
```

## Logging

Log Files For StartUp Scripts Are Written To Folder
`/data/data/alsultan.shell/rootfs/usr/var/log/boot`