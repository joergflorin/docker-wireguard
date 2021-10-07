# homebridge

Docker service definitions for homebridge server.

Create subdirectories `moneymoney` (only private access) and `munki_repo` (public read access) as samba shares.

Set environment variables for setting the users for the directories:

`export SMBUSER=MyUser`
`export SMBPASS=MyPassword`

Finally run following command in this directory: 

`docker-compose up -d`