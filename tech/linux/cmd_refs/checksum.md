# checksum commands

## See also
- [openssl](./openssl.md)

###### calculate md5 checksum
```bash
md5sum file
```

###### calculate sha256 checksum
```bash
sha256sum file
```

###### calculate checksum of disc (where `xxxxxxxx` is the size of the iso file in bytes from which the disc was burned)
```bash
dd if=/dev/cdrom bs=1 count=xxxxxxxx | sha256sum
```

