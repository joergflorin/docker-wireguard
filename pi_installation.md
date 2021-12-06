# Installation of Raspberry PI for running docker in my environment
 
## Install PI image
 
see https://www.raspberrypi.org/documentation/computers/getting-started.html
 
1. Download Raspbery Pi Imager
2. Start Imager
3. Select newest Pi OS Lite (32-Bit)
4. Ctrl-Shift-X for advanced options
   - set hostname (e.g. mypi)
   - configure ssh access

## Mount external drive (fuse, ntfs) for full backups only (optional)

### Install ntfs-3g driver
```
sudo apt-get install ntfs-3g
```

### Configure mount point

1. Get UUID via command `blkid` -> my-complete-uuid
2. Create mount point

```
sudo mkdir /mnt/my-external-mount
```

3. Add to `/etc/fstab`

```
PARTUUID=my-complete-uuid /mnt/my-external-mount     ntfs    defaults,noauto,nls=utf-8        0       0
```

The drive can be mounted by following command

```
sudo mount /mnt/my-external-mount
```

## Install git

```sudo apt-get install git
