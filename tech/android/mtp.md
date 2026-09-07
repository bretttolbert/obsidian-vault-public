# mtp (android USB connectivity)

###### MTP file transfer troubleshooting

- Try a Data Cable: Some USB cables are strictly for charging and lack the data pins necessary for MTP. Try swapping the cable and using a dedicated data transfer cable.

###### Force kill MTP Services
```bash
killall gvfs-mtp-volume-monitor
```

###### Start MTP Services
```bash
systemctl --user start gvfs-mtp-volume-monitor.service
```

###### Restart MTP Services

```bash
systemctl --user restart gvfs-mtp-volume-monitor.service
```

Additionally, disconnect phone from USB, then reconnect USB and set mode to file transfer again.

###### Force MTP Device Detection

```bash
mtp-detect
```

###### Install MTP Libraries and Drivers

```bash
sudo apt update
sudo apt install mtp-tools libmtp-common libmtp-runtime libmtp9 gvfs-backends jmtpfs
```
