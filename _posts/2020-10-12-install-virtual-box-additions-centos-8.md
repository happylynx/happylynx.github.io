# Install Virtual Box Additions in CentOS 8

1. Running VM window menu > Devices > Insert Guest Additions CD Image ...
2. mount the CD image
   ```
   sudo mkdir -p /mnt/cdrom
   sudo mount /dev/cdrom /mnt/cdrom
   ```
3. install dependencies
   ```
   sudo dnf install -y bzip2 tar elfutils-libelf-devel gcc perl kernel-headers kernel-devel
   ```
4. run the installer
   ```
   sudo /mnt/cdrom/VBoxLinuxAdditions.run
   ```
   If you see error like
   ```
   ValueError: File context for /opt/VBoxGuestAdditions-6.1.14/other/mount.vboxsf already defined
   modprobe vboxguest failed
   The log file /var/log/vboxadd-setup.log may contain further information.
   ```
   your system is likely missing some of the dependencies.

   If you system uses only text mode, use
   ```
   sudo /mnt/cdrom/VBoxLinuxAdditions.run --nox11
   ```

## Mounting of shared directory

```
sudo mount -t vboxsf -o uid=${id -u} gid=${id -g} <shared-dir-name> <mountpoint-dir>
```

`-o uid=${id -u} gid=${id -g}` allows user and group remapping to the current user.
