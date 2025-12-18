# Disabling IPv6

I usually do this by modifying the preference values in `/etc/gai.conf`,

but that didn't work for my Banana Pi. Instead, this worked:

Add the following to `/etc/sysctl.conf` and reboot:


```bash
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
```
