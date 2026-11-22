# FTP Server: pure-ftpd

## See also
- [tftp](./tftp.md)

###### Set up an FTP server (pure-ftpd)
```bash
#install pure-ftpd (for Polycom phone configs)
#add universe repository (if needed)
#append this to /etc/apt/sources.list:
deb http://us.archive.ubuntu.com/ubuntu/ saucy universe
deb-src http://us.archive.ubuntu.com/ubuntu/ saucy universe
deb http://us.archive.ubuntu.com/ubuntu/ saucy-updates universe
deb-src http://us.archive.ubuntu.com/ubuntu/ saucy-updates universe
#refresh package manager:
sudo apt-get update
#install pure-ftpd
sudo apt-get install pure-ftpd
(Per https://help.ubuntu.com/community/PureFTP)
sudo groupadd ftpgroup
sudo useradd -g ftpgroup -d /dev/null -s /etc ftpuser
sudo mkdir /var/ftproot
sudo chown -R ftpuser:ftpgroup /var/ftproot
sudo pure-pw useradd polycomftp -u ftpuser -d /var/ftproot
#set the password to "password" when prompted
sudo pure-pw useradd brett -u ftpuser -d /var/ftproot
#set the password to "brett" when prompted
sudo pure-pw mkdb
sudo ln -s /etc/pure-ftpd/pureftpd.passwd /etc/pureftpd.passwd
sudo ln -s /etc/pure-ftpd/pureftpd.pdb /etc/pureftpd.pdb
sudo ln -s /etc/pure-ftpd/conf/PureDB /etc/pure-ftpd/auth/PureDB
sudo service pure-ftpd restart
```