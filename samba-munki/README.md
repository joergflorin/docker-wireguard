# samba-munki

Docker service definitions for Samba server.

Create subdirectories `moneymoney` (only private access) and `munki_repo` (public read access) as samba shares.

Set environment variables for setting the users for the directories:

Admin user for read/write access to both directories:

```
export SMBUSER_ADMIN=AdminUser
export SMBPASS_ADMIN=AdminPassword
```

MoneyMoney user for read/write access just to the `moneymoney` directory:

```
export SMBUSER_MM=MMUser
export SMBPASS_MM=MMPassword
```

Finally run following command in this directory: 

```
docker-compose up -d
```

see https://hub.docker.com/r/trnape/rpi-samba/
