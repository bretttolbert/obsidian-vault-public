# Banana Pi

###### Fix for _stretch Release "does not have a Release file"_

Update `/etc/apt/sources.list` from

```bash
deb http://raspbian.raspberrypi.org/raspbian/ stretch main contrib non-free rpi
```

to

```bash
deb http://legacy.raspbian.org/raspbian/ stretch main contrib non-free rpi
```

###### Fix for _apt-add-repository: command not found_

```bash
sudo apt install software-properties-common
```

###### Auto-start the terminal

To auto-start the terminal on boot, open this file with nano:

```bash
nano ~/.config/lxsession/LXDE-pi/autostart
```

Add this line to the end of the file:

```bash
@lxterminal
```

