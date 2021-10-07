# http-munki

Docker service definitions for nginx http server.

The nginx server will share the directory `./samba-munki/munki_repo` from the samba server as http root. This directory contains
the munki repository with installers and manifests for deploying mac software. Run following command in this directory: 

`docker-compose up -d`