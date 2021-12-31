# http-munki

Docker service definitions for speedtest.

The speedtest use the local config directory. Run following command in this directory: 

```
docker-compose up -d
```

After installing you will need to download the speedtest binary and extract it in the directory `config/www/app/Bin`, see https://github.com/peanutbother/docker-speedtest/issues/1.

see https://hub.docker.com/r/bricksoft/speedtest
