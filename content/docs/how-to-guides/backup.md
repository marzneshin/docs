---
title: "Backup"
---

### Steps to Backup Marzneshin Files

{{< callout type="info" >}}
It's good practice to backup your Marzneshin files regularly to prevent data loss in case of system failures.
{{< /callout >}}

1. **Backup Important Files:**
   - By default, all Marzneshin important files are saved in `/var/lib/marzneshin` (Docker versions).
   - Copy the entire `/var/lib/marzneshin` directory to a backup location of your choice, such as an external hard drive or cloud storage.

2. **Backup Configuration Files:**
   - Make sure to backup your env file, which contains your configuration variables.
   - If you installed Marzneshin using the script (recommended installation approach), the env and other configurations should be inside `/etc/opt/marzneshin/` directory.

{{< callout type="error" >}}
Failure to perform regular backups may result in data loss, which is not recoverable. Ensure you maintain frequent backups to safeguard your data.
{{< /callout >}}

### Backup Directory Structure

{{< filetree/container >}}
  {{< filetree/folder name="var" >}}
    {{< filetree/folder name="lib" >}}
      {{< filetree/folder name="marzneshin" >}}
      {{< /filetree/folder >}}
    {{< /filetree/folder >}}
  {{< /filetree/folder >}}
  {{< filetree/folder name="etc" >}}
    {{< filetree/folder name="opt" >}}
      {{< filetree/folder name="marzneshin" >}}
        {{< filetree/file name="env" >}}
      {{< /filetree/folder >}}
    {{< /filetree/folder >}}
  {{< /filetree/folder >}}
{{< /filetree/container >}}

By following these steps, you can ensure that you have a backup of all your Marzneshin files and data, as well as your configuration variables and Xray configuration, in case you need to restore them in the future. Remember to update your backups regularly to keep them up-to-date.

