# Commands for Debian flavors of Linux e.g. Ubuntu

## See also
- [ubuntu](./ubuntu.md)

###### Restart networking
```bash
sudo systemctl restart networking
```

###### List status of all services (ubuntu):
```bash
services --status-all
```

###### Edit network configuration (Debian)
```bash
sudo vim /etc/network/interfaces
```

###### Install a Debian package directly
```bash
sudo dpkg -i package.deb
```

###### Search installed packages:
```bash
dpkg -l | grep package
```

###### Remove installed package:
```bash
sudo dpkg -r package
```

###### See files installed by a package
```bash
dpkg-query -L package
```

###### Search for packages to install (Debian)
```bash
apt-cache search package
```
Note: You don't need to use wildcards, it will list partial matches.

###### Search for packages with names beginning with "tcl"
```bash
apt-cache search ^tcl
```

###### Install a package (Debian)
```bash
sudo apt-get install package
```

###### List all installed packages and filter by name
```bash
apt list --installed | grep python
```

###### Add a repository (Debian)
```bash
sudo vim /etc/apt/sources.list
sudo apt-get update
```

###### Add a PPA (Ubuntu)
```bash
sudo add-apt-repository ppa:videolan/stable-daily
```

###### Install apt-file
```bash
sudo apt-get install apt-file
```

###### Search all packages for filename
```bash
apt-file search filename
```

###### Remove and purge packages matching wildcard
```bash
sudo apt-get remove --purge vlc*
```
