# Misc. Linux commands

###### Fix mouse cursor in Ubuntu 23.04

Set the following environment variable:

```bash
QT_QPA_PLATFORM=xcb
```

Add it to `/etc/environment` to make it permanent.

###### byte-by-byte comparison
```bash
cmp file1 file2
```

###### Banner
```bash
$ banner brett

 #####   #####   ######   #####   #####
 #    #  #    #  #          #       #
 #####   #    #  #####      #       #
 #    #  #####   #          #       #
 #    #  #   #   #          #       #
 #####   #    #  ######     #       #


```

###### Whatis command - show one-line description of given Linux command
```bash
$ whatis sudo
sudo (8)             - execute a command as another user
$ whatis apt
apt (8)              - command-line interface
$ whatis ping
ping (8)             - send ICMP ECHO_REQUEST to network hosts
```

###### Pipe command output directly to clipboard
```bash
somecommand | xclip -selection clipboard
```

###### Factor an integer
```bash
$ factor 5280
5280: 2 2 2 2 2 3 5 11
$ factor 1080
1080: 2 2 2 3 3 3 5
$ factor 360
360: 2 2 2 3 3 5
$ factor 12
12: 2 2 3

```

###### Calendar
```
$ cal
     March 2022       
Su Mo Tu We Th Fr Sa  
       1  2  3  4  5  
 6  7  8  9 10 11 12  
13 14 15 16 17 18 19  
20 21 22 23 24 25 26  
27 28 29 30 31        
```

###### Bash Calculator
```bash
$ bc
bc 1.07.1
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006, 2008, 2012-2017 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
2+2
4

```

###### Shutdown immediately
```bash
sudo shutdown now
```

###### Display current logged in user's username
```bash
whoami
```

###### List all currently logged in users (method 1)
```bash
who
```

###### List all currently logged in users (method 2)
```bash
w
```

###### Send a message to all users
```bash
wall "server going down for reboot in 10 minutes"
```

###### Shortcut (alias) for `ls -l`
```bash
ll
```

###### Human-readable format for sizes, e.g. `197M` instead of `206354132` 
```bash
ll -h
```

###### Change directory to home directory
```bash
cd ~
```

###### Change directory to home directory of user named bob
```bash
cd ~bob
```

###### Change directory to the parent directory
```bash
cd ..
```

###### Change directory to the previous directory
```bash
cd -
```

###### Diff two directories and only print differences
```bash
diff -qr dir1/ dir2/
```
- `-q` quiet
- `-r` recursive

###### Show memory usage of processes
```bash
top
```

###### Create a symlink
```bash
ln -s /path/to/target /path/to/symlink
```

###### Show disk usage of files in current directory
```bash
du -sch *
```
- `-c` display total (**cumulative space**)
- `-s` single-directory, i.e. don't recursively compute space of subdirectories
- `-h` human-readable

##### Show disk space usage
```bash
df -h
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           1.6G  2.0M  1.6G   1% /run
/dev/sda5       428G   75G  332G  19% /
tmpfs           7.9G  432K  7.9G   1% /dev/shm
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
/dev/sdb1       1.9T  1.1T  780G  59% /data
tmpfs           1.6G  1.7M  1.6G   1% /run/user/1000
```

###### Show free memory
```bash
free -h
```

##### Show Linux version using the LSB (Linux Standard Base) Release command
```bash
lsb_release -a
```
- `-a` display all information
- `-d` description (single-line)
- `-r` release

###### See which process is using a port
```bash
lsof -i :5000
```

###### List all open files by a given PID (in this case `1234`)
```bash
lsof -p 1234
```

###### Use xdotool to emulate a key press
```bash
sudo apt-get install xdotool xbase-clients
xdotool key ctrl+shift+t
```

###### Open a file in the default application
```bash
xdg-open filename
```

###### Open a file in the default application in the background
```bash
xdg-open filename &
```

###### Open GUI File Browser at the current directory
```bash
xdg-open .
```

###### List files sorted alphabetically by the 2nd field
```bash
ls -l | sort -k2
```

###### List files sorted numerically by the 5th field
```bash
ls -l | sort -n5
```

###### List files sorted by size
```bash
ls -lS
```

###### List files with classifier (* after executable files)
```bash
ls -F
```

###### Count the number of lines of output
```bash
pylama -l pep8,import_order src test | wc -l
```

###### Print the exit code of the previous command
```bash
$ echo $?
127
```

###### Display the first two lines of a file:

Method 1:
```bash
pi@raspberrypi ~ $ head -n 2 wxtest.py
#!/usr/bin/env pythonf
import wx
pi@raspberrypi ~ $
```

Method 2:
```bash
pi@raspberrypi ~ $ cat wxtest.py | sed -n '1,2p'
#!/usr/bin/env python
import wx
pi@raspberrypi ~ $
```

###### Show only unique lines (in this example, unique IP addresses in a pcap)
```bash
tshark -r capture.pcapng -T fields -e ip.src | sort -u
```

###### tr - Translate characters
```bash
echo 'I LovE linuX. one is better Than 2' | tr "a-z" "A-Z"
```

###### tail - Display the last line of a file
```bash
pi@raspberrypi ~ $ tail -n 1 /var/log/dmesg
[   23.748486] bcm2835-cpufreq: switching to governor ondemand
pi@raspberrypi ~ $
```

###### Convert tabs to spaces - Using expand
```bash
expand -t 4 src-tabs.py > src-spaces.py
```

###### Convert tabs to spaces - Using sed
```bash
sed -i 's/\t/    /g' <file>
```

###### Use stream redirection operators to combine stderr (2) and stdout (1) into the stdout stream for further manipulation
```bash
g++ lots_of_errors.cpp 2>&1 | head
```

Note: 
- `>&` is the syntax to redirect a stream to another file descriptor.
- `0` is stdin
- `1` is stdout
- `2` is stderr

###### Append (send in addition)
```bash
echo "some text" >> file.txt
```

###### Replace (send to as a whole completed file)
```bash
echo "some text" > file.txt
```

###### Trim leading and trailing whitespace
```bash
echo " test test " | sed -e 's/^ *//g' -e 's/ *$//g'
```

###### Remove all whitespace
```bash
echo " test test " | tr -d ' '
```

###### Create a virtual python environment with specified interpreter
```bash
virtualenv -p /usr/bin/python2.6 path/to/new/virtualenv/
```

###### Turn off system bell
```bash
xset b off
```

###### Add user to group
```bash
usermod -a -G group user
```

###### Remove user from group
```bash
gpasswd -d user group
```

###### List all the groups that a user belongs to (2 ways)
```bash
groups user
getent group
```

###### Identify location of executable
```bash
which python
```

###### Determine where a program resides
```bash
$ which tclsh
/usr/bin/tclsh
$ whereis tclsh
tclsh: /usr/bin/tclsh8.5 /usr/bin/tclsh /usr/bin/X11/tclsh8.5 /usr/bin/X11/tclsh /usr/share/man/man1/tclsh.1.gz 
```

###### List all environment variables
```bash
env
```

###### List all exported variables and functions
```bash
export -p
```

###### Time a command (measure execution time)
```bash
$ time my_script.sh

real    0m17.401s
user    0m3.076s
sys     0m4.384s
```

###### Display current date and time
```bash
$ date
Sun Mar  9 17:01:08 CDT 2014
```

###### Set date and time
```bash
date -s "2 OCT 2006 18:00:00"
```

###### Display NTP associations
```bash
ntpq -p
```

###### Display NTP date
```bash
ntpdate
```

###### Check if a process (ntpd) is running
```bash
ps -f -C ntpd
```

###### Make terminal bigger
```bash
stty cols 220 rows 60
```

###### Shorten bash terminal prompt 
```bash
export PS1="\u@\h \w$ "
```

###### Shorten your bash terminal prompt, more
```bash
export PS1='\u@\h$ '
```

###### Really shorten your bash terminal prompt
```bash
export PS1='$ '
```

###### Retype a command from history without executing it
```bash
!1234:p
```

###### Set terminal tab background color (DARKRED)
```bash
echo -ne '\e]11;#560505\a'
```

###### List the 10 most recently entered commands
```bash
history 10
```

###### Search command history
```bash
history | grep pattern
```

###### Set the DISPLAY environment variable
```bash
export DISPLAY=:0 
```
If you're launching a GUI program from an SSH terminal, you may need to run the above command first.

###### Open gedit in the background without it spewing debug into the terminal
```bash
gedit PCAP.py > /dev/null 2>&1 &
```

###### Edit bash configuration file
```bash
vim ~/.bashrc
```

###### Edit xserver configuration file
```bash
vim ~/.xinitrc
```

###### Edit SSH server configuration file
```bash
sudo vim /etc/ssh/sshd_config
```

###### SSH with verbose output for troubleshooting
```bash
ssh -v user@host
```

###### View syslog
```bash
tail -f /var/log/syslog
```

###### View auth log
```bash
tail -f /var/log/auth.log
```

###### Display X monitor infok
```bash
xrandr
```

###### Set display position
```bash
xrandr --output VBOX0 --left-of VBOX1
```


Step 1 - copy Modeline from output of the following command:
```bash
cvt 1920 1080
```

Step 2 - Add a new mode
```bash
xrandr --newmode <Modeline>
```

E.g.
```bash
$ xrandr --newmode "1920x1080_60.00"   173.00  1920 2048 2248 2576  1080 1083 1088 1120 -hsync +vsync
```

Or use this one-liner:
```bash
xrandr --newmode $(cvt 1920 1080 | sed -n -e 's/^.*Modeline //p')
```

Step 3 - Add mode to monitor
```bash
xrandr --addmode VBOX0 <ModeName>
```

```bash
$ xrandr --addmode VBOX0 1920x1080_60.00
```

Step 4 - Set monitor mode
```bash
xrandr --output VBOX0 --mode <ModeName>
```

See: [How to change display resolution settings using xrandr](http://www.ubuntugeek.com/how-change-display-resolution-settings-using-xrandr.html)


###### Inspect a command with the `type` command
```bash
type <cmd>
```
- If it's a program or script, it will give you it's location. 
- If it's an alias, it will tell you what it's aliased to.
- If it's a function, it will print the function; 
- otherwise, it will tell you if it is a built-in or a keyword.

###### Links

* [Debian NetworkConfiguration](https://wiki.debian.org/NetworkConfiguration)
* [Debian NetworkConfiguration - Bringing up and interface without an IP address](https://wiki.debian.org/NetworkConfiguration#Bringing_up_an_interface_without_an_IP_address)
* [How do I set up dual monitors in xfce](http://askubuntu.com/questions/62681/how-do-i-setup-dual-monitors-in-xfce)

###### Recursively change owner of a directory
```bash
sudo chown -R user:pass dir
```

###### Display system uptime
```bash
user@OPGX270MVT1:~$ uptime
 14:58:32 up  2:00,  4 users,  load average: 0.18, 0.10, 0.12
```

###### List all mounted devices
```bash
mount
```

###### List usb verbosely
```bash
lsusb -v
```

###### Open a serial console to the specified serial port using the `cu` (*call up*) program:
```bash
cu -l /dev/ttyS0 -s 9600
```

###### To exit serial console *call up* program (`cu`), type:
```bash
~.
```

###### Perform a basic port scan with nmap
```bash
nmap -A -T4 <host>
```

###### Switch between tabs in gnome-terminal, gedit, and some other programs
```bash
Alt + n
```
Where n is the tab number. 1=1st tab, 2=2nd tab, etc.

###### random vs. urandom
- random - will block if the entropy pool is empty
- urandom - will generate data using an algorithm if entropy pool is empty, will never block.

[random vs. urandom](http://stupefydeveloper.blogspot.com/2007/12/random-vs-urandom.html)

###### Clean package manager (try this if you are having issues)
```bash
sudo apt-get clean
```

###### Add a user
```bash
sudo useradd admin
```

###### Set password
```bash
sudo passwd admin
```

###### Add a user to sudoers
```bash
sudo adduser admin sudo
```

###### Delete a user
```bash
sudo userdel admin
```

###### Remove user from suders
```bash
sudo deluser admin sudo
```

###### Enable the root account
```bash
sudo passwd root
```

###### Setuid

[wikipedia: setuid](http://en.wikipedia.org/wiki/Setuid)

###### Setting the `setgid` permission on a directory
```bash
chmod g+s
```
This causes new files and subdirectories created within it to inherit its group ID, rather than the primary group ID of the user who created the file (the owner ID is never affected, only the group ID). 

###### Get UUID of drive
```bash
sudo blkid
```

###### Get info about graphics card and drive
```bash
inxi -Gx
```

###### List software and hardware blocks on wireless adapters
```bash
rfkill list all
```

###### Watch a directory for changes
```bash
watch -d ls -ltr
```
- `watch -d` watch a command (e.g. `ls -ltr`) and display the differences
- `ls -l` long format output (details)
- `ls -t` sort by modified time
- `ls -r` reverse sort order, i.e. show most recently modified first

###### iostat
```bash
$ iostat
Linux 5.13.0-35-generic (brett-Z68XP-UD4)    03/13/2022     _x86_64_  (8 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           2.50    0.01    0.55    0.19    0.00   96.75

Device             tps    kB_read/s    kB_wrtn/s    kB_dscd/s    kB_read    kB_wrtn    kB_dscd
loop0             0.00         0.02         0.00         0.00       1949          0          0
loop1             0.01         0.05         0.00         0.00       5762          0          0
loop10            0.01         0.02         0.00         0.00       2961          0          0
loop11            0.01         0.03         0.00         0.00       3032          0          0
loop12            0.01         0.02         0.00         0.00       2339          0          0
loop13            0.01         0.02         0.00         0.00       2333          0          0
loop14            0.00         0.02         0.00         0.00       2554          0          0
loop15            0.00         0.01         0.00         0.00       1144          0          0
loop16            0.00         0.01         0.00         0.00       1155          0          0
loop17            0.00         0.00         0.00         0.00        421          0          0
loop18            0.00         0.00         0.00         0.00        427          0          0
loop19            0.01         0.37         0.00         0.00      44691          0          0
loop2             0.00         0.02         0.00         0.00       1939          0          0
loop20            0.01         0.26         0.00         0.00      31375          0          0
loop21            0.00         0.01         0.00         0.00        869          0          0
loop3             0.00         0.00         0.00         0.00         17          0          0
loop4             0.00         0.04         0.00         0.00       4821          0          0
loop5             0.00         0.01         0.00         0.00        987          0          0
loop6             0.00         0.01         0.00         0.00        922          0          0
loop7             0.01         0.02         0.00         0.00       2310          0          0
loop8             0.00         0.02         0.00         0.00       2954          0          0
loop9             0.00         0.00         0.00         0.00         51          0          0
sda               2.46        16.91        61.68         0.00    2031314    7407336          0
sdb               0.29         7.87         0.00         0.00     945271          0          0
sdc               0.18         3.44         0.69         0.00     413291      83226          0
sr0               0.00         0.00         0.00         0.00          1          0          0


```

###### List kernel modules
```
kmod list
```

###### pstree - process tree
```
$ pstree
systemd─┬─ModemManager───2*[{ModemManager}]
        ├─NetworkManager───2*[{NetworkManager}]
        ├─accounts-daemon───2*[{accounts-daemon}]
        ├─acpid
        ├─agetty
        ├─avahi-daemon───avahi-daemon
        ├─colord───2*[{colord}]
        ├─cron
        ├─cups-browsed───2*[{cups-browsed}]
        ├─cupsd
        ├─dbus-daemon
        ├─dockerd─┬─containerd───13*[{containerd}]
        │         └─14*[{dockerd}]
        ├─firefox─┬─10*[Isolated Web Co───26*[{Isolated Web Co}]]
        │         ├─Isolated Web Co───32*[{Isolated Web Co}]
        │         ├─Isolated Web Co───39*[{Isolated Web Co}]
        │         ├─Isolated Web Co───27*[{Isolated Web Co}]
        │         ├─Isolated Web Co───28*[{Isolated Web Co}]
        │         ├─Privileged Cont───26*[{Privileged Cont}]
        │         ├─RDD Process───10*[{RDD Process}]
        │         ├─Socket Process───5*[{Socket Process}]
        │         ├─2*[Web Content───18*[{Web Content}]]
        │         ├─Web Content───19*[{Web Content}]
        │         ├─WebExtensions───27*[{WebExtensions}]
        │         └─160*[{firefox}]
        ├─gnome-keyring-d─┬─ssh-agent
        │                 └─3*[{gnome-keyring-d}]
        ├─gsd-printer───2*[{gsd-printer}]
        ├─ibus-daemon─┬─ibus-engine-sim───2*[{ibus-engine-sim}]
        │             ├─ibus-extension-───3*[{ibus-extension-}]
        │             ├─ibus-memconf───2*[{ibus-memconf}]
        │             ├─ibus-ui-gtk3───3*[{ibus-ui-gtk3}]
        │             └─2*[{ibus-daemon}]
        ├─ibus-x11───3*[{ibus-x11}]
        ├─irqbalance───{irqbalance}
        ├─2*[kerneloops]
        ├─lightdm─┬─Xorg───{Xorg}
        │         ├─lightdm─┬─gnome-session-b─┬─budgie-daemon───3*[{budgie-daemon}]
        │         │         │                 ├─budgie-extras-d───3*[{budgie-extras-d}]
        │         │         │                 ├─budgie-panel─┬─dropover───3*[{dropover}]
        │         │         │                 │              └─11*[{budgie-panel}]
        │         │         │                 ├─budgie-polkit-d───3*[{budgie-polkit-d}]
        │         │         │                 ├─budgie-wm───3*[{budgie-wm}]
        │         │         │                 ├─evolution-alarm───5*[{evolution-alarm}]
        │         │         │                 ├─gdmcheck.sh
        │         │         │                 ├─gnome-screensav───3*[{gnome-screensav}]
        │         │         │                 ├─gsd-a11y-settin───3*[{gsd-a11y-settin}]
        │         │         │                 ├─gsd-color───3*[{gsd-color}]
        │         │         │                 ├─gsd-datetime───3*[{gsd-datetime}]
        │         │         │                 ├─gsd-disk-utilit───2*[{gsd-disk-utilit}]
        │         │         │                 ├─gsd-housekeepin───3*[{gsd-housekeepin}]
        │         │         │                 ├─gsd-keyboard───3*[{gsd-keyboard}]
        │         │         │                 ├─gsd-media-keys───3*[{gsd-media-keys}]
        │         │         │                 ├─gsd-power───3*[{gsd-power}]
        │         │         │                 ├─gsd-print-notif───2*[{gsd-print-notif}]
        │         │         │                 ├─gsd-rfkill───2*[{gsd-rfkill}]
        │         │         │                 ├─gsd-screensaver───2*[{gsd-screensaver}]
        │         │         │                 ├─gsd-sharing───3*[{gsd-sharing}]
        │         │         │                 ├─gsd-smartcard───3*[{gsd-smartcard}]
        │         │         │                 ├─gsd-sound───3*[{gsd-sound}]
        │         │         │                 ├─gsd-usb-protect───3*[{gsd-usb-protect}]
        │         │         │                 ├─gsd-wacom───3*[{gsd-wacom}]
        │         │         │                 ├─gsd-wwan───3*[{gsd-wwan}]
        │         │         │                 ├─gsd-xsettings───3*[{gsd-xsettings}]
        │         │         │                 ├─indicator-appli───2*[{indicator-appli}]
        │         │         │                 ├─kdeconnectd───6*[{kdeconnectd}]
        │         │         │                 ├─nemo-desktop───3*[{nemo-desktop}]
        │         │         │                 ├─nm-applet───3*[{nm-applet}]
        │         │         │                 ├─plank───3*[{plank}]
        │         │         │                 ├─update-notifier───3*[{update-notifier}]
        │         │         │                 ├─windowshufflerd───3*[{windowshufflerd}]
        │         │         │                 └─4*[{gnome-session-b}]
        │         │         └─2*[{lightdm}]
        │         └─2*[{lightdm}]
        ├─mount.ntfs
        ├─nemo───3*[{nemo}]
        ├─networkd-dispat
        ├─packagekitd───2*[{packagekitd}]
        ├─polkitd───2*[{polkitd}]
        ├─power-profiles-───2*[{power-profiles-}]
        ├─rhythmbox───12*[{rhythmbox}]
        ├─rsyslogd───3*[{rsyslogd}]
        ├─rtkit-daemon───2*[{rtkit-daemon}]
        ├─sd_dummy───2*[{sd_dummy}]
        ├─sd_espeak-ng───4*[{sd_espeak-ng}]
        ├─showtime_deskto───4*[{showtime_deskto}]
        ├─snapd───14*[{snapd}]
        ├─speech-dispatch───2*[{speech-dispatch}]
        ├─sublime_text─┬─plugin_host-3.3───2*[{plugin_host-3.3}]
        │              ├─plugin_host-3.8───2*[{plugin_host-3.8}]
        │              └─20*[{sublime_text}]
        ├─systemd─┬─(sd-pam)
        │         ├─at-spi-bus-laun─┬─dbus-daemon
        │         │                 └─3*[{at-spi-bus-laun}]
        │         ├─at-spi2-registr───2*[{at-spi2-registr}]
        │         ├─bamfdaemon───4*[{bamfdaemon}]
        │         ├─dbus-daemon
        │         ├─dconf-service───2*[{dconf-service}]
        │         ├─evolution-addre───5*[{evolution-addre}]
        │         ├─evolution-calen───8*[{evolution-calen}]
        │         ├─evolution-sourc───3*[{evolution-sourc}]
        │         ├─goa-daemon───3*[{goa-daemon}]
        │         ├─goa-identity-se───2*[{goa-identity-se}]
        │         ├─gvfs-afc-volume───3*[{gvfs-afc-volume}]
        │         ├─gvfs-goa-volume───2*[{gvfs-goa-volume}]
        │         ├─gvfs-gphoto2-vo───2*[{gvfs-gphoto2-vo}]
        │         ├─gvfs-mtp-volume───2*[{gvfs-mtp-volume}]
        │         ├─gvfs-udisks2-vo───3*[{gvfs-udisks2-vo}]
        │         ├─gvfsd─┬─gvfsd-dnssd───2*[{gvfsd-dnssd}]
        │         │       ├─gvfsd-network───3*[{gvfsd-network}]
        │         │       ├─gvfsd-trash───2*[{gvfsd-trash}]
        │         │       └─2*[{gvfsd}]
        │         ├─gvfsd-fuse───5*[{gvfsd-fuse}]
        │         ├─gvfsd-metadata───2*[{gvfsd-metadata}]
        │         ├─ibus-portal───2*[{ibus-portal}]
        │         ├─pipewire───{pipewire}
        │         ├─pipewire-media-───{pipewire-media-}
        │         ├─pulseaudio───3*[{pulseaudio}]
        │         ├─tilix─┬─bash───pstree
        │         │       └─10*[{tilix}]
        │         ├─xdg-desktop-por───6*[{xdg-desktop-por}]
        │         ├─xdg-desktop-por───3*[{xdg-desktop-por}]
        │         ├─xdg-document-po─┬─fusermount
        │         │                 └─6*[{xdg-document-po}]
        │         └─xdg-permission-───2*[{xdg-permission-}]
        ├─systemd-journal
        ├─systemd-logind
        ├─systemd-resolve
        ├─systemd-timesyn───{systemd-timesyn}
        ├─systemd-udevd
        ├─thermald───{thermald}
        ├─udisksd───4*[{udisksd}]
        ├─unattended-upgr───{unattended-upgr}
        ├─upowerd───2*[{upowerd}]
        ├─whoopsie───2*[{whoopsie}]
        └─wpa_supplicant
```