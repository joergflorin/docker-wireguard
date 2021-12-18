# http-munki

Docker service definitions for backup the whole home directory with rsnapshot.

You have to create a file `env.txt` in this directory containg one statement:

```
BACKUP_DIR=/my/backup/root/directory
```

You also have to configure the backup settings in `./config/rsnapshot.conf` and `./config/crontabs/root`.

```
./install.sh
```

see https://hub.docker.com/r/linuxserver/rsnapshot
