# Networking

## See also
- [ipconfig](./ipconfig.md)
- [iptables](./iptables.md)
- [netstat](./netstat.md)
- [networking](./networking.md)
- [ping](./ping.md)

###### Hostname
```bash
hostname
```

###### Show listening TCP and UDP sockets
```bash
netstat -tulpn
```
- `-tulpn` (the ugly limo parked next door)
- `-t` tcp - show UDP sockets
- `-u` udp - show TCP sockets
- `-l` listening - show listening sockets
- `-p` program - show the PID
- `-n` numeric - show the address

###### Check the nameservers
```bash
$ nmcli -t -f IP4.DNS device show eth0
IP4.DNS[1]:192.168.1.1
IP4.DNS[2]:8.8.8.8
```
or
```bash
cat /etc/resolv.conf
```

###### Nmap scan of local network
```bash
nmap -sP 192.168.1.0/24
```

###### Nmap TCP SYN scan of host
```bash
nmap -sS 10.6.199.5
```

###### Display interface status
```bash
ifconfig -a
```

###### To display the routing table you can use any of the following methods:


###### route command
```bash
sudo route -n
```

###### netstat command
```bash
netstat -rn
```

###### ip route list command
```bash
ip route list
```

###### netstat -nux command
```bash
netstat -nux
```

###### netstat options
```bash
-a : all
-e : extended info
-r : --route : display kernel IP routing table
-n : --numeric : diplay numerically (don\'t resolve names)
-i : display interface stats
-t : --tcp : display only TCP connections
-u : --upd : display only UDP connections
-x : --unix : unix sockets
-w : --raw : raw sockets
-v : --verbose : verbose output
```

[wikipedia: netstat](https://en.wikipedia.org/wiki/Netstat)

###### Check for incoming packets from a host
```bash
sudo tcpdump -nnxX -i eth0 src 10.17.199.251
```

###### Scan a subnet for open web servers
```bash
nmap -p 80 --open -sV 10.17.199.0/24
```

###### Configure firewall
```bash
iptables -D INPUT 6
iptables --list
service iptables save
iptables-save > /etc/sysconfig/iptables
iptables -A INPUT -j DROP
iptables -A OUTPUT -j DROP
iptables -A FORWARD -j DROP
iptables -I INPUT 6 -p tcp --dport 443 -j ACCEPT
service iptables save
```

###### Location of networking files (Red Hat)
```bash
/
  etc
    crontab    
    inittab
    fstab
    hosts    
    rc.local
    resolv.conf
    init.d
      iptables
    sysconfig
      iptables-config
    network
      interfaces
      network-scripts
        ifcfg-eth0
        route-eth0
      wpa-supplicant
    httpd
      conf
      conf.d
  var
    www
      html
```


## gai.conf prefer IPv4

### Force apt-get to prefer IPv4 - append the following to /etc/gai.conf:
```bash
precedence ::ffff:0:0/96  100
```
References:
- [Convince apt get not to use IPv6](http://unix.stackexchange.com/questions/9940/convince-apt-get-not-to-use-ipv6-method)
- [gai.conf](http://linux.die.net/man/5/gai.conf) is the getaddrinfo configuration file


## To remove all IP addresses from an interface
```bash
sudo ip addr flush dev eth1
```

## Add a static route
```bash
ip route add 10.10.10.0/24 via 192.168.1.254 dev eth1
```

## setcap

### Set the raw sockets capability on the python interpreter executable:
```bash
sudo setcap 'CAP_NET_RAW+eip CAP_NET_ADMIN+eip' /usr/bin/python2.7
sudo setcap 'CAP_NET_RAW+eip CAP_NET_ADMIN+eip' /usr/sbin/tcpdump
```


### Edit the udev rules to change the names of network adapters

* Step 1. Determine the MAC addresses of the interfaces
```bash
ifconfig -a
```
* Step 2. Edit udev rules
```bash
sudo vim /etc/udev/rules.d/70-persistent-net.rules
```
- See: [Linux Rename Eth0 Network Interface Card Names using Udev](http://www.cyberciti.biz/faq/howto-linux-rename-ethernet-devices-named-using-udev/)

```bash
Configuration file '/etc/X11/Xsession.d/98vboxadd-xclient'
 ==> Modified (by you or by a script) since installation.
 ==> Package distributor has shipped an updated version.
   What would you like to do about it ?  Your options are:
    Y or I  : install the package maintainer's version
    N or O  : keep your currently-installed version
      D     : show the differences between the versions
      Z     : start a shell to examine the situation
 The default action is to keep your current version.
*** 98vboxadd-xclient (Y/I/N/O/D/Z) [default=N] ? 
Setting up virtualbox-guest-dkms (4.3.36-dfsg-1+deb8u1ubuntu1.14.04.1) ...
Loading new virtualbox-guest-4.3.36 DKMS files...
Building only for 3.13.0-24-generic
```
