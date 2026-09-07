# nginx

## View live traffic (Access Log)
```bash
tail -f /var/log/nginx/access.log
```

## View recent errors (Error Log)
```bash
tail -f /var/log/nginx/error.log
```

## View systemd log
```bash
journalctl -u nginx
```

## Test configuration
```bash
$ nginx -t
2026/08/24 17:54:30 [warn] 11692#11692: the "user" directive makes sense only if the master process runs with super-user privileges, ignored in /etc/nginx/nginx.conf:1
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
2026/08/24 17:54:30 [emerg] 11692#11692: open() "/run/nginx.pid" failed (13: Permission denied)
nginx: configuration file /etc/nginx/nginx.conf test failed
```
