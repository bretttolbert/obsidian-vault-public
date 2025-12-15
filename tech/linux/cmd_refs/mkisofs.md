# mkisofs

###### Create ISO image from directory
```bash
mkisofs -J -l -R -V "name" -iso-level 4 -o name.iso {dir}
```

###### Create ISO image from disc
- requires root
- must unmount first
```bash
blocks=$(isosize -d 2048 /dev/sr0)
sudo dd if=/dev/sr0 of=/tmp/output.iso bs=2048 count=$blocks status=progress
```

