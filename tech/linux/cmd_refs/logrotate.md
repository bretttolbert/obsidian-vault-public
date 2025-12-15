# logrotate

### logrotate configuration

Config file: `/etc/logrotate.conf`
Config dir: `/etc/logrotate.d/*`

Files in config dir are applied in alphanumeric order, so the last one may override anything in the others (if unscoped).

```bash
compress
delaycompress
maxsize 50M
minsize 100k
missingok
notifempty
rotate 4
weekly
```

### Cron jobs

logrotate is invoked by the daily cron job (`/etc/cron.daily/logrotate`). Copy to `/etc/cron.hourly/logrotate` to run hourly.

### Fill syslog (for test purposes)

```bash
#!/bin/bash
while true; do
    logger "test msg"
    head -c 5000 < /dev/zero | tr '\0' '\142' | logger
done
```

First need to disable imjournalctl throttling, by adding the following to `/etc/rsyslog.conf`:
```bash
$imjournalRatelimitInterval 0
$imjournalRatelimitBurst 0
```

### Test logrotate

Note: `--debug` makes it do a _dry run_ without actually rotating anything.

```bash
logrotate --debug --force /etc/logrotate.conf > logrotate_debug_out.txt
logrotate --force /etc/logrotate.conf > logrotate_out.txt
```
