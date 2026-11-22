# systemd

## List timers

```bash
sudo systemctl list-timers --all
```

## Template for a systemd unit file (e.g. `/etc/systemd/system/banana.service`)

```bash
[Unit]
Description=Run Banana Privileged Script
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/banana_script.sh
# Define your environment variable here
Environment="BANANA_USER=monkey"

[Install]
WantedBy=multi-user.target

```

## Template for a systemd timer file (e.g. `/etc/systemd/system/banana.timer`)


```bash
[Unit]
Description=Run Banana Script Hourly

[Timer]
# Option A: Run exactly at the start of every hour (e.g., 1:00, 2:00)
OnCalendar=hourly

# Option B: Alternatively, run exactly 1 hour after the last time it finished
# OnUnitActiveSec=1h

# Helps distribute system load by allowing a 5-minute window for execution
AccuracySec=5m
# Ensures it catches up immediately if the system was shut down when it should have run
Persistent=true

[Install]
WantedBy=timers.target

```

## How to enable it and start it

```bash
# Reload systemd to detect the new configuration files
sudo systemctl daemon-reload

# Enable the timer so it starts automatically on system boot
sudo systemctl enable banana.timer

# Alternatively, enable it now:
sudo systemctl enable --now your-timer-name.timer

# Start the timer immediately right now
sudo systemctl start banana.timer

```


## View the real-time execution logs and check for your environment variable errors:

```bash
sudo journalctl -u banana.service -f
```

