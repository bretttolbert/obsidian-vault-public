# Linux SFTP Server

### Installation Steps


###### Step 1: Install OpenSSH Server

```bash
sudo apt install openssh-server
```

###### Step 2: Modifying the SSHD Configuration for the SFTP Group

Append this to `/etc/ssh/sshd_config`:

```bash
Match group sftp
ChrootDirectory /home
X11Forwarding no
AllowTcpForwarding no
ForceCommand internal-sftp -l VERBOSE -f LOCAL6
```

- Runs the internal SFTP server with log level _verbose_ to syslog channel name `LOCAL6`

###### Step 3: Restart SSH services

```bash
sudo systemctl restart sshd
```

###### Step 4: Create an SFTP Group

```bash
sudo addgroup sftp
```

###### Step 5: Create a new SFTP user

```bash
sudo useradd -m sftp_user -g sftp
sudo passwd sftp_user
```

###### Step 6: Restrict Access to the User's Home Directory

```bash
sudo chmod 700 /home/sftp_user/
```

###### Step 7: Test it

```bash
sftp sftp_user@localhost
```

###### Step 8: Set up bind mount(s) for desired folders

I use a bind mount to make my `/data/Music` folder accessible from within the SFTP chroot.

```bash
sudo mkdir -p /home/sftp_user/Music
sudo chown -R `whoami`:`whoami` /home/sftp_user/Music
sudo mount -o remount,ro,bind /data/Music /home/sftp_user/Music
```

SFTP should show the same contents for both directories. Bind mounts are a common way to make directories available inside chroots.

To make it persistent, add an fstab entry e.g.

```bash
/media/brett/Data/Music /home/sftp_user/Music none defaults,bind 0 0
```

Complete `/etc/fstab` file:

```
brett@pentatonic:~$ cat /etc/fstab 
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/sda5 during installation
UUID=24d706c9-426b-4d67-9d80-ed896f59b986 /               ext4    errors=remount-ro 0       1
UUID=3262DCAB62DC7557 /media/brett/Data ntfs-3g rw,nosuid,nodev,relatime,nofail,errors=remount-r,x-gvfs-show,uid=1000,gid=1000,iocharset=utf8,windows_names 0 0
/media/brett/Data/Music /home/sftp_user/Music none defaults.bind 0 0
/media/brett/Data/MusicOther /home/sftp_user/MusicOther none defaults,bind 0 0
/media/brett/Data/MusicPartyMix1 /home/sftp_user/MusicPartyMix1 none defaults,bind 0 0
/media/brett/Data/MusicPartyMix2 /home/sftp_user/MusicPartyMix2 none defaults,bind 0 0
/media/brett/Data/MusicPartyMix3 /home/sftp_user/MusicPartyMix3 none defaults,bind 0 0
/home/brett/Git/obsidian-vault-private /home/sftp_user/Git/obsidian-vault-private none defaults,bind 0 0
/home/brett/Git/misc /home/sftp_user/Git/misc none defaults,bind 0 0
/media/brett/Data/Shared /home/sftp_user/Shared none defaults,bind 0 0
```


To test fstab:

```bash
sudo mount -a
```

Cautionary Tale: In my environment, `/data/Music` is a symlink to the real directory `/media/brett/Data`. Do not use a symlink in `/etc/fstab` or it will fail to mount on boot as I found out when I attempted to use `/data/Music`. The symlink works when running the `mount` command because I've already booted and `/media/brett/Data` is mounted and `mount -a` works as well with a symlink in `/etc/fstab`, deceivingly.

Here's my full fstab, inlcluding my custom entry to mount my `data` drive:

```bash
brett@pentatonic:/etc/ssh$ cat /etc/fstab 
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/sda5 during installation
UUID=24d706c9-426b-4d67-9d80-ed896f59b986 /               ext4    errors=remount-ro 0       1
UUID=3262DCAB62DC7557 /media/brett/Data ntfs-3g rw,nosuid,nodev,relatime,nofail,errors=remount-r,x-gvfs-show,uid=1000,gid=1000,iocharset=utf8,windows_names 0 0
/media/brett/Data/Music /home/sftp_user/Music none defaults,bind 0 0
/media/brett/Data/MusicOther /home/sftp_user/MusicOther none defaults,bind 0 0
/media/brett/Data/MusicPartyMix1 /home/sftp_user/MusicPartyMix1 none defaults,bind 0 0
/media/brett/Data/MusicPartyMix2 /home/sftp_user/MusicPartyMix2 none defaults,bind 0 0
/media/brett/Data/MusicPartyMix3 /home/sftp_user/MusicPartyMix3 none defaults,bind 0 0
/home/brett/Git/obsidian-vault-private /home/sftp_user/Git/obsidian-vault-private none defaults,bind 0 0
/home/brett/Git/misc /home/sftp_user/Git/misc none defaults,bind 0 0
```
