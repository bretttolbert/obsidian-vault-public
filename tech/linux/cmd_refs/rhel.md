# Commands for Red Hat flavors of linux (e.g. RHEL, Fedora, CentOS, ALMA, etc.)

###### Restart networking
```bash
sudo systemctl restart network
```

###### Display Red Hat version
```bash
cat /etc/redhat-release
```

###### Search for packages to install (RHEL)
```bash
yum list package
```
Note: If you don't know the exact name, use wildcards e.g. yum list *gtk*

###### Install a package (RHEL)
```bash
su -c 'yum -y install package' 
```

