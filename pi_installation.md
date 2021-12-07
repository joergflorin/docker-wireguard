# Installation of Raspberry PI for running docker in my environment
 
## Install PI image
 
see https://www.raspberrypi.org/documentation/computers/getting-started.html
 
1. Download Raspbery Pi Imager
2. Start Imager
3. Select newest Pi OS Lite (32-Bit)
4. Ctrl-Shift-X for advanced options
   - set hostname (e.g. mypi)
   - configure ssh access
5. Boot pi with prepared SD card and connect via ssh
6. update os:

```
sudo apt-get update
sudo apt-get dist-upgrade
sudo apt-get autoclean
```

## Mount external drive (fuse, ntfs) for full backups only (optional)

### Install ntfs-3g driver

`sudo apt-get install ntfs-3g`

### Configure mount point

1. Get UUID via command `blkid` -> my-complete-uuid
2. Create mount point

`sudo mkdir /mnt/my-external-mount`

3. Add to `/etc/fstab`

`PARTUUID=my-complete-uuid /mnt/my-external-mount     ntfs    defaults,noauto,nls=utf-8        0       0`

The drive can be mounted by following command

`sudo mount /mnt/my-external-mount`

## Install git

`sudo apt-get install git`

## Install and configure docker
see https://docs.docker.com/engine/install/debian/

### Install docker
https://docs.docker.com/engine/install/debian/#install-using-the-convenience-script

### Add user pi to group docker

`sudo usermod -aG docker ${USER}`
### Running docker at system boot

`sudo systemctl enable docker`

### Install docker-compose
see https://pumpingco.de/blog/setup-your-raspberry-pi-for-docker-and-docker-compose/

```
sudo apt-get install libffi-dev libssl-dev
sudo apt install python3-dev
sudo apt-get install -y python3 python3-pup
sudo pip3 install docker-compose
```

## Configure and install containers
### Portainer CE
https://docs.portainer.io/v/ce-2.9/
https://docs.portainer.io/v/ce-2.9/start/install/server/docker/linux

http address of portainer: http://mypi:9000

### clone repository with docker compose configurations to /home/pi

```
cd
git clone https://github.com/joergflorin/docker
```

### SMB file server
via docker-yaml, see https://github.com/joergflorin/docker/tree/master/samba-munki

### nginx http server
via docker-yaml, see https://github.com/joergflorin/docker/tree/master/http-munki

### homebridge
via docker-yaml, see https://github.com/joergflorin/docker/tree/master/homebridge

### cron trigger for external websites
via docker-yaml, see https://github.com/joergflorin/docker/tree/master/scheduler

## ddclient (for external ipv6 access)
`sudo apt-get install ddclient`

Configuration:
```
usev6=if, if=eth0
protocol=dyndns2
server=dyndns.strato.com
login=mystratoid
password='myddnspassword'
myexternaldomain.de
```

Configure ipv6 of mypi for access through the router.
