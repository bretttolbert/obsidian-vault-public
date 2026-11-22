# tftp - Trivial File Transfer Protocol

## See also
- [ftp](./ftp.md)

## Install tftpd-hpa TFTP server

```bash
sudo apt-get install tftpd-hpa
```

Create root directory and set the permissions (the lazy way)
```bash
sudo mkdir /var/tftpboot
sudo chmod 777 /var/tftpboot
```

Edit configuration file
```bash
/etc/default/tftpd-hpa
TFTP_USERNAME="tftp"
TFTP_DIRECTORY="/var/tftpboot"
TFTP_ADDRESS="0.0.0.0:69"
TFTP_OPTIONS="-s -c -v"
RUN_DAEMON="yes"
```

Restart service
```bash
sudo service tftpd-hpa start
```

Source: [install TFTP server on linux](http://www.cesareriva.com/install-tftp-server-on-linux/)

