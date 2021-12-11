# homebridge

Docker service definitions for homebridge server.

Create a subdirectory `homebridge` for storing config data and run following command in this directory: 

```
docker-compose up -d
```

Copy preinstalled Modules to `~/docker/homebridge/homebridge/node_modules`

Auth file in `~/docker/homebridge/homebridge/auth.json`

Configuration file in `~/docker/homebridge/homebridge/config.json`

Installed Plugins:

- Homebridge Fritz Platform (homebridge-fritz-platform)
- Homebridge RPi (homebridge-rpi)
- Homebridge WoL (homebridge-wol)

see https://hub.docker.com/r/oznu/homebridge
