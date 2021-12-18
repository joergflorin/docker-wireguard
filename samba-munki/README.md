# samba-munki

Docker service definitions for Samba server.

Create subdirectories `moneymoney` (only private access) and `munki_repo` (public read access) as samba shares. 

Set environment variables for setting the users for the directories in the new file `env.txt` in this directory:

Admin user for read/write access to both directories:

```
SMBUSER_ADMIN=AdminUser
SMBPASS_ADMIN=AdminPassword
```

MoneyMoney user for read/write access just to the `moneymoney` directory:

```
SMBUSER_MM=MMUser
SMBPASS_MM=MMPassword
```

Finally run following command in this directory: 

```
./install.sh
```

see https://hub.docker.com/r/trnape/rpi-samba/
