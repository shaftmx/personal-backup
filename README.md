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
* If you want use ssh with password you need sshpass.
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


You can also customize things like : 

Change the logfile path
    LOGFILE="/tmp/personal-backup.log"
    
    # User ssh pour le serveur de backup
    # SSH_user="root"
    # SSH_addr="127.0.0.1"
    
    # SSH password need : apt-get install sshpass N'utilise pas si pas déclaré
    #SSH_password="mypassword"
    
    # UUID du disque de backup
    #ExternalBackupUUID="" TODO check que l'uid est dans la liste blkid
    #ExternalMountPoint=""  # Ckeck que le device de l'uuid est bien monté dans mointpoint
    #ExternalKeepMounted="yes"
    
    # Serveur backup address and directory (destination du backup
    BDirs="/tmp/back/" 
    
    # post-command commande aprés rsync (serveur ou locale)  N'utilise pas si pas déclaré
    #POST_COMMAND="chown -R 1000:1000 $BDirs"
    # Ou par exemple avec des notification  apt-get install libnotify-bin
    #POST_COMMAND="sudo -u gael notify-send -t 999999999 'backup end'"
    
    # Rsync extended args permet d'ajouter des arguments, par exemple des filtres voir exemple
    RSYNC_args=""
    
    # Mode verbose
    #verbose=""    # o

Exemple of rsync args with filter :
    RSYNC_args="--filter '- /video/films' --filter '- /video/series'"

