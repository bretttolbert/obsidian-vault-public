# Raspberry Pi

###### Open Raspberry Pi configuration menu
```bash
sudo raspi-config
```

###### Modify Raspberry Pi configuration file
```bash
sudo vim /boot/config.txt
```

###### Play a video (Raspberry Pi)
```bash
omxplayer myvideo.mp4
```

###### View an image (Raspberry Pi)
```bash
gpicview myimage.jpg
```

###### Use WiringPi to display status of GPIO 0
```bash
pi@raspberrypi ~ $ gpio readall | grep "GPIO 0"
|      0   |  17  |  11  | GPIO 0 | IN   | Low   |
pi@raspberrypi ~ $
```

###### Display the value ("High" or "Low") of GPIO 0
```bash
pi@raspberrypi ~ $ gpio readall | grep "GPIO 0" | sed -e 's/\s*|\s*/\n/g' | sed -n '7p'
Low
pi@raspberrypi ~ $
```

###### Naming scheme for Raspberry Pi's

- "A" models have no on-board Ethernet and only 1 USB header
- "B" models have on-board Ethernet and 1 or 2 USB headers (2 and 4 ports, respectively)
- "B+" models have an additional onboard USB header (max 2 headers, for 4 ports)


