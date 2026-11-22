# cryptsetup (Front-end for LUKS)

## How to  an external drive with LUKS

Source: https://opensource.com/article/21/3/encryption-luks

### 1. Find your drive

Use `lsblk -f` to find your drive, e.g. `/dev/sdb`

```bash
$ lsblk
sda    8:0    0 111.8G  0 disk 
sda1   8:1    0 111.8G  0 part /
sdb    8:112  1  57.6G  0 disk 
sdb1   8:113  1  57.6G  0 part /mydrive
sdX    8:128  1   1.8G  0 disk 
sdX1   8:129  1   1.8G  0 part
```

Make sure you identify the correct drive because encrypting it overwrites everything on it. My drive is not empty, but it contains copies of documents I have copies of elsewhere, so losing this data isn't significant to me.

### 2. Clear the drive

To proceed, destroy the drive's partition table by overwriting the drive's head with zeros:

```bash
$ sudo dd if=/dev/zero of=/dev/sdX count=4096
```

This step isn't strictly necessary, but I like to start with a clean slate.

### 3. Format your drive for LUKS

The `cryptsetup`` command is a frontend for managing LUKS volumes. The luksFormat subcommand creates a sort of LUKS vault that's password-protected and can house a secured filesystem.

When you create a LUKS partition, you're warned about overwriting data and then prompted to create a passphrase for your drive:

```bash
$ sudo cryptsetup luksFormat /dev/sdX
WARNING!
========
This will overwrite data on /dev/sdX irrevocably.

Are you sure? (Type uppercase yes): YES
Enter passphrase: 
Verify passphrase:
```

### 4. Open the LUKS volume

Now you have a fully encrypted vault on your drive. Prying eyes, including your own right now, are kept out of this LUKS partition. So to use it, you must open it with your passphrase. Open the LUKS vault with cryptsetup open along with the device location (/dev/sdX, in my example) and an arbitrary name for your opened vault:

```bash
$ cryptsetup open /dev/sdX vaultdrive
```

I use vaultdrive in this example, but you can name your vault anything you want, and you can give it a different name every time you open it.

LUKS volumes are opened in a special device location called `/dev/mapper`. You can list the files there to check that your vault was added:

```bash
$ ls /dev/mapper
control  vaultdrive
```

You can close a LUKS volume at any time using the close subcommand:

```bash
$ cryptsetup close vaultdrive
```

This removes the volume from /dev/mapper.

### 5. Create a filesystem

Now that you have your LUKS volume decrypted and open, you must create a filesystem there to store data in it. In my example, I use ext4, but you can use XFS or JFS or any filesystem you want:

```bash
$ sudo mkfs.ext4 -L myvault /dev/mapper/vaultdrive
```

### Mount and unmount a LUKS volume

You can mount a LUKS volume from a terminal with the mount command. Assume you have a directory called /mnt/hd and want to mount your LUKS volume there:

```bash
$ sudo cryptsetup open /dev/sdX vaultdrive
$ sudo mount /dev/mapper/vaultdrive /mnt/hd
```

LUKS also integrates into popular Linux desktops. For instance, when I attach an encrypted drive to my workstation running KDE or my laptop running GNOME, my file manager prompts me for a passphrase before it mounts the drive.

