# ntfsfix

###### How to fix NTFS drive that won't mount rw
First you need to umount the drive. 
E.g. by clicking the *eject* button in the GUI menu or `umount /data` where `/data` is the mount point.
Then run the following commands:
```bash
sudo ntfsfix /dev/sdXY
sudo mount -a
```
