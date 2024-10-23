---
title: "Backup"
weight: 1
---

It's always a good idea to backup your Marzneshin files regularly to prevent data loss in case of system failures or
accidental deletion. Here are the steps to backup Marzneshin:

1. By default, all Marzneshin important files are saved in `/var/lib/marzneshin` (Docker versions). Copy the
   entire `/var/lib/marzneshin` directory to a backup location of your choice, such as an external hard drive or cloud
   storage.
2. Additionally, make sure to backup your env file, which contains your configuration variables. If you installed
   Marzneshin using the script (recommended installation approach), the env and other configurations should be
   inside `/etc/opt/marzneshin/` directory.

By following these steps, you can ensure that you have a backup of all your Marzneshin files and data, as well as your
configuration variables and Xray configuration, in case you need to restore them in the future. Remember to update your
backups regularly to keep them up-to-date.
