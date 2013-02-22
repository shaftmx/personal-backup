Personal-backup
===================

Package source. Backup your computer on remote host or external device with rsync. 


Features
---------
* Backup targets by ssh 
* Backup targets in custom directory
* Backup targets in external device
* Mmount / umount external device
* Launch postbackup command
* Add rsync args like filter


Usage
--------

    Usage: $0: [OPTIONS]
      -b                  : Start backup
      -d                  : List external devices
      -m                  : Mount the external devices
      -u                  : Umount the external devices
      -v                  : Verbose mode
      -h                  : Show help


Installation
-------------

### Manual

You just need to copy personal-backup script into a directory in your **$PATH**.

The next thing is to put the config file personal-backup.conf in **/etc**.

* You need **rsync** indeed.
* If you want use ssh with password you need **sshpass**.
* If you want use an external device you need **util-linux** for blkid command

### Package

The package has not yet repo but you can build with tools like pbuilder

Configuration
-------------
TODO - Finish this doc

After the installation you need to configure personal-backup.
    
Enable personal-backup (default security) need to be 1

    enable="0"

Directories you want backup

    Target="/dir1 /dir2"

Chose the backup directory where you want to push your data. Used for all backups (external, ssh, local).

    BDirs="/tmp/back/"

Configure user and host for ssh backup

    SSH_user="root"
    SSH_addr="127.0.0.1"

If you want a backup on a external device you can specify the UUID and the mountpoint. The uuid is given by **personal-backup -d**

    ExternalBackupUUID="94ea7e38-5d29-4824-bb0f-e20b7856d90d"
    ExternalMountPoint="/media/backup"

**You can also customize things like :**


Change the logfile path

    LOGFILE="/tmp/personal-backup.log"

Specify a password for ssh

    SSH_password="mypassword"

When you use a external backup you can umount or keep mounted the external device

    ExternalKeepMounted="yes"

Launch a post backup command on remote ssh server or local for local backups.

    POST_COMMAND="sudo -u gael notify-send -t 60 'backup end'"

Add custom args in rsync like exclude or filter for exemple

    RSYNC_args="--filter '- /video/films' --filter '- /video/series'"

