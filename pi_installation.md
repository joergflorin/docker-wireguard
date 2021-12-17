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
6. Install `~/.ssh/authorized_keys` for easy ssh access.
7. update os:

```
sudo apt-get update
sudo apt-get dist-upgrade
sudo apt-get autoclean
sudo reboot
```

## istatserver

https://bjango.com/help/istat3/linuxpackages/

https://github.com/bjango/istatserverlinux

```
curl -fsSL https://raw.githubusercontent.com/bjango/istatserverlinux/master/get-istatserver.sh -o istatserverlinux.sh && sh istatserverlinux.sh

```

### Enabling istatserver on system boot

Download https://raw.githubusercontent.com/bjango/istatserverlinux/master/resource/systemd/istatserver.service

```
curl -fsSL https://raw.githubusercontent.com/bjango/istatserverlinux/master/resource/systemd/istatserver.service -o istatserver.service
sudo cp istatserver.service /etc/systemd/system/istatserver.service
sudo chmod 755 /etc/systemd/system/istatserver.service
sudo systemctl enable istatserver
sudo reboot
```

Find or change istatserver code in `/usr/local/etc/istatserver/istatserver.conf`

## Mount external flash drive (fuse, exfat) for optional full backups

### Install exfat driver

```
sudo apt-get install exfat-fuse
sudo apt-get install exfat-utils
```

### Configure mount point

#### Determine UUID

```
sudo blkid
sudo blkid -o list -w /dev/null
```

-> my-complete-uuid

#### Create mount point

```
sudo mkdir /media/my-external-mount
```

#### Configure `/etc/fstab`

```
PARTUUID=my-complete-uuid /media/my-external-mount exfat defaults,noauto,umask=000,users,rw 0 0
```

## Install git

```
sudo apt-get install git
```

## Install and configure docker
see https://docs.docker.com/engine/install/debian/

### Install docker
https://docs.docker.com/engine/install/debian/#install-using-the-convenience-script

```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

### Add user pi to group docker

```
sudo usermod -aG docker ${USER}
```

### Running docker at system boot

```
sudo systemctl enable docker
```

The pi should be rebooted now.

### Install docker-compose
see https://pumpingco.de/blog/setup-your-raspberry-pi-for-docker-and-docker-compose/

```
sudo apt-get install libffi-dev libssl-dev
sudo apt install python3-dev
sudo apt-get install -y python3 python3-pip
sudo pip3 install docker-compose
```

## Configure and install containers
### Portainer CE
https://docs.portainer.io/v/ce-2.9/
https://docs.portainer.io/v/ce-2.9/start/install/server/docker/linux

http address of portainer: https://mypi:9443

Upgrading: https://docs.portainer.io/v/ce-2.9/start/upgrade/docker

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
```
sudo apt-get install ddclient
```

Configuration (`/etc/ddclient.conf`):
```
usev6=if, if=eth0
protocol=dyndns2
server=dyndns.strato.com
login=mystratoid
password='myddnspassword'
myexternaldomain.de
```

Configure ipv6 of mypi for access through the router:

```
ip addr show dev eth0 | sed -e's/^.*inet6 \([^ ]*\)\/.*$/\1/;t;d'
```

The shown full address has the prefix of the router und the last four words should be configured in the sharing setting of the router. E.g output is:

```
1111:2222:3333:4444:5555:6666:7777:8888
9999::aaaa:bbbb:cccc:dddd
```

`1111:2222:3333:4444` is the prefix of the router and `5555:6666:7777:8888` is the IPv6 interface address of the rPi.
