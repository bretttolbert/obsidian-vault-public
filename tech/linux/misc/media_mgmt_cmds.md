# My favorite Linux commands for managing my music library 

Contents:
- Various commands for working with SD cards, as that's how I get mp3s onto my android phone.
- Batch scripts with rsync commands for backing up music to external hard drives and copying to SD cards

Tips:
- Always use your android phone to format SD cards. I ran into a lot of problems using Linux (gnome-disks) to FAT format the cards. E.g. transfers failing midway through due to filesystem corruption. I've had much better success using Android Files app to format the card. Using `fatlabel` to change the SD card volume label seems to work fine though.

###### Get bpm of media file

```bash
bpm-tag -f -n file.mp3
```

###### Rename `album.jpg` to `cover.jpg`, recursively

```bash
# Install rename
sudo apt install -y rename

# Get before counts
find /data/Music -type f -iname album.jpg | wc # output: some value A
find /data/Music -type f -iname cover.jpg | wc # output: some value C

# Rename
find /data/Music -iname "album.jpg" -exec rename 's/album.jpg/cover.jpg/' '{}' \;

# Get after counts
find /data/Music -type f -iname album.jpg | wc # output: 0
find /data/Music -type f -iname cover.jpg | wc # output: A + C

# Repeat for album.png, if you have any (or convert them)
# Also check for Cover.jpg, using find -name Cover.jpg
```

###### Convert `wav` to `mp3`

```bash
ffmpeg -i file.wav -c:a libmp3lame -vn -ar 44100 -ac 2 -b:a 320k file.mp3
```

###### Convert container from `mkv` to `mp4` without reencoding video but reencode audio (e.g. from opus) to aac

```bash
ffmpeg -i video.mkv -vcodec copy -acodec aac -b:a 320k video.mp4
```

###### Convert container from `mkv` to `mp4` and reencode video to H265

```bash
ffmpeg -i video.mkv -c:v libx265 -c:a aac -b:a 320k video.mp4
```

###### Convert container from `mkv` to `mp4` and reencode video to H265, scaling to 1080p

```bash
ffmpeg -i video.mkv -c:v libx265 -c:a aac -b:a 320k -vf "scale=1920:1080" video.mp4
```

###### Convert container from `mkv` to `mp4` and reencode video to H265, cropping (e.g. from 1920x1440) to 1080p (1920x1080) (ffmpeg will automatically center it)

```bash
ffmpeg -i video.mkv -c:v libx265 -c:a aac -b:a 320k -vf "crop=1920:1080" video.mp4
```

###### Convert container from `mkv` to `mp4` and reencode video to H265, padding (e.g. from 1440x1080) to 1080p (1920x1080) (ffmpeg will not automatically center it)

```bash
ffmpeg -i video.mkv -c:v libx265 -c:a aac -b:a 320k -vf "pad=1920:1080:(ow-iw)/2:(oh-ih)/2" video.mp4
```

###### Merge audio and video, keeping video codec and reencoding audio to aac

```bash
ffmpeg -i video.mp4 -i audio.webm -c:v copy -c:a aac merged.mp4
```

###### Merge audio and video, converting video from vp9 to H.264 and reencoding audio from Opus to aac

```bash
ffmpeg -i video.webm -i audio.webm -c:v libx264 -c:a aac merged.mp4
```

###### Download youtube video (download best quality video and best quality audio and merge them)

```bash
youtube-dl -k -f 'bestvideo[fps<=30]+bestaudio' <url>
```

###### Download youtube playlist starting at specified video index

```bash
youtube-dl -k -f 'bestvideo[fps<=30]+bestaudio' --yes-playlist --playlist-start <idx> <url>
```

###### Sort all files by filesize (recursively)
```bash
ls -lSR | sort -k 5 -n
```

###### Tip: For Windows compatibility, ensure no colons in dir or filenames
```bash
brett@brett-Z68XP-UD4:/data/Music$ find . -name "*:*"
./David McCallum/Music: A Bit More of Me [1968]
./Michael Jackson/HIStory: Past, Present and Future, Book I [1995]
./Three 6 Mafia/When the Smoke Clears: Sixty 6, Sixty 1 [2000]
./Trick Daddy/Thug Matrimony: Married to the Streets [2005]
./White Zombie/La Sexorcisto : Devil Music Vol. 1 [1992]
```

###### Rsync Music to Raspberry Pi from Windows (Linux)

```bash
rsync -ahPv /data/Music/ brett@192.168.0.119:/home/brett/Music/ --delete --prune-empty-dirs --exclude "Brett Tolbert"
```

###### Rsync Music to Raspberry Pi from Windows (MINGW64/Git Bash)

```bash
rsync -ahPv /d/Music/ brett@192.168.0.119:/home/brett/Music/ --delete --prune-empty-dirs --exclude "Brett Tolbert"
```

###### Backup commands (Windows)

```
robocopy D:\Music\ F:\Music /mir /v
robocopy D:\Music\ H:\Music /mir /v /xd "D:\Music\Brett Tolbert"
robocopy D:\Music\ "C:\Users\Brett\My Drive\Music" /mir /v
```

###### MTP

MTP paths look like this:
```
mtp://LGE_LM-V600_LMV600VM27c849fe/SD%20card
```

However, to run rsync, we need the path. It can be found like this:

```bash
$ cd /run/user/$UID/gvfs/mtp*
$ pwd
/run/user/1000/gvfs/mtp:host=LGE_LM-V600_LMV600VM27c849fe
```

And the path to the Music folder:
```bash
/run/user/1000/gvfs/mtp:host=LGE_LM-V600_LMV600VM27c849fe/SD\ card/Music/
```


###### Reset android media scan database
- Must enable developer mode first
- Can be executed via USB debugging or LADB
```
pm clear com.android.providers.media.module
```


###### Command to change volume label on exFAT (android) formatted SD card
`gnome-disks` utility always sets it to uppercase, if you want lowercase, use `fatlabel`
```bash
$ sudo fatlabel /dev/sdc1 
ANDROID
$ sudo fatlabel /dev/sdc1 android
fatlabel: warning - lowercase labels might not work properly on some systems
$ sudo fatlabel /dev/sdc1 
android
```

###### How to fix NTFS drive that won't mount rw

1. First you need to umount the drive e.g. `umount /data` where `/data` is the mount point.

2. Next find the device name using `fdisk -l` e.g.:

```
Disk /dev/sdb: 1.82 TiB, 2000398934016 bytes, 3907029168 sectors
Disk model: WDC WD20EURS-63S
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0x7557764f

Device     Boot Start        End    Sectors  Size Id Type
/dev/sdb1        2048 3907026943 3907024896  1.8T  7 HPFS/NTFS/exFAT
```

3. Run the `ntfsfix` command on the device:

```bash
sudo ntfsfix /dev/sdb1
```

4. Mount the drive you unmounted in step 1:

```bash
sudo mount -a
```

###### Copy incoming music to Music
```bash
rsync -ahPv ~/Downloads/incoming/ /data/Music/
```

###### Compare directories (`-n` = dry run)
```bash
rsync -avnc /data/Music/ /media/brett/My\ Book/Music/ --delete | grep "^deleting "
```

###### `BackupMusic`
```bash
#!/bin/bash
rsync -ahPv /data/Music/ /media/brett/My\ Book/Music/ --delete --prune-empty-dirs
rsync -ahPv /data/MusicFLAC/ /media/brett/My\ Book/MusicFLAC/ --delete --prune-empty-dirs
rsync -ahPv /data/MusicWAV/ /media/brett/My\ Book/MusicWAV/ --delete --prune-empty-dirs
rsync -ahPv /data/MusicOther/ /media/brett/My\ Book/MusicOther/ --delete --prune-empty-dirs
```

###### `SyncMusicToSDCard`
```bash
#!/bin/bash
SDVOLUME=android
USER=brett
mkdir -p /media/$USER/$VOLUME/Music
cmd="rsync -ahPv /data/Music/ /media/$USER/$SDVOLUME/Music/ --delete --prune-empty-dirs --ignore-existing"
eval "$cmd"
while [ $? -ne 0 ]; do
    eval "$cmd"
done

```
Explanation: I added the *retry until sucessful* loop because rsync often fails to write to SD cards with errors such as this one (restarting rsync works in this case):
```
Indochine/7000 Danses/07 Un Grand Carnaval.mp3
         32.77K   1%    1.12MB/s    0:00:01  rsync: [receiver] rename "/media/brett/android/Music/Indochine/7000 Danses/.05 Les tzars.mp3.C3Wkul" -> "Indochine/7000 Danses/05 Les tzars.mp3": No such file or directory (2)
rsync: [receiver] rename "/media/brett/android/Music/Indochine/7000 Danses/.06 La Machine A Rattraper Le Temps.mp3.IfdO8u" -> "Indochine/7000 Danses/06 La Machine A Rattraper Le Temps.mp3": No such file or directory (2)

rsync: [sender] write error: Broken pipe (32)
rsync error: error in socket IO (code 10) at io.c(823) [sender=3.2.3]
rsync error: received SIGUSR1 (code 19) at main.c(1592) [generator=3.2.3]

```
or in this case restarting rsync doensn't work:
```
unouomedude/IGIF Presents_ Endless Summer Vol. I/
rsync: [receiver] mkstemp "/media/brett/android/Music/Voxtrot/Biggest Fan/.AlbumArtSmall.jpg.rszYIc" failed: Read-only file system (30)
```
I have tried zeroing the cards with DD and then reformatting using the gnome-disks utility (FAT format) for my android phone. Maybe I should use ext4, since android supports it.

> [Android has always supported the FAT32, Ext3, and Ext4 file system formats](https://knowtechie.com/which-file-systems-can-android-read/)

It uses exFAT though... Here's what a 256 GB micro SD card formatted by my android phone looks like
exFat (version 1.0) according to the gnome-disks utility
```
Disk /dev/sdc: 250 GiB, 268436504576 bytes, 524290048 sectors
Disk model: SD/MMC          
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x00000000

Device     Boot Start       End   Sectors  Size Id Type
/dev/sdc1        2048 524290014 524287967  250G  7 HPFS/NTFS/exFAT
```

###### Pulsar+ rescan media library
In Pulsar+, click the triple dot button on the top right and you will find an option to rescan your media library. I reccommend running this after adding media to your SD card.


###### `SyncObsidianVaultToSDCard`
```bash
#!/bin/bash
SDVOLUME=android
USER=brett
mkdir -p /media/$USER/$SDVOLUME/Git/obsidian-vault-private
rsync -avh /home/$USER/Git/obsidian-vault-private/ \
    /media/$USER/$SDVOLUME/Git/obsidian-vault-private/ --delete --prune-empty-dirs --exclude=.git
```

###### `CountAudioFiles`
```bash
#!/bin/bash

USER=$USER
SDVOLUME=android
EXTHDDVOLUME="My Book"

count_audio_files () { source PrintAudioFiles "$1" | wc -l; }

echo /data/Music
count_audio_files /data/Music

echo /media/$USER/$EXTHDDVOLUME/Music
count_audio_files "/media/$USER/$EXTHDDVOLUME/Music"

echo /media/$USER/$SDVOLUME/Music
count_audio_files /media/$USER/$SDVOLUME/Music
```

###### `PrintAudioFiles`
```bash
#!/bin/bash
# expect argument: $1 - base dir path to search for music
# prints each file path, excluding the base bir path
find "$1" -type f \( -iname "*.mp3" -o -iname "*.m4a" \) -print
```

###### `PrintGenres`
```bash
#!/bin/bash
find $1 -type f \( -iname "*.mp3" -o -iname "*.m4a" \) -exec ffprobe {} \; 2>&1 | egrep "genre" | sort | uniq -c | sort -rn -k1.4,7
```

###### `Shuffle1`
```bash
#!/bin/bash
source PrintAudioFiles "$1" | shuf -n 1 | xargs --delimiter '\n' vlc --play-and-exit
```

###### `ShuffleForever`
```bash
#!/bin/bash
while :
do
    source Shuffle1 "$1"
done
```

######  Get working Music dir and backup Music dir sizes
```bash
$ du -hs /data/Music/
50G    /data/Music/

$ du -hs /media/brett/My\ Book/Music/
59G    /media/brett/My Book/Music/

$ du -hs /media/brett/android/Music/
52G	   /media/brett/android/Music/
```

######  Diff Music directories
```bash
diff -qr /data/Music/ /media/brett/My\ Book/Music/
```

###### Backup music to Kodi / LibreElec
```bash
rsync -ahPv /data/Music/ root@192.168.0.186:/storage/music/ --delete --prune-empty-dirs --exclude "Brett Tolbert"
rsync -ahPv /data/MusicVideos/ root@192.168.0.186:/storage/musicvideos/ --delete --prune-empty-dirs
```

######  Backup mp3/m4a Music (delete files that no longer exist in source)
```bash
rsync -ahPv /data/Music/ /media/brett/My\ Book/Music/ --delete --prune-empty-dirs
```

######  Backup other Music folders
```bash
rsync -ahPv /data/MusicFLAC/ /media/brett/My\ Book/MusicFLAC/ --delete --prune-empty-dirs
rsync -ahPv /data/MusicWAV/ /media/brett/My\ Book/MusicWAV/ --delete --prune-empty-dirs
rsync -ahPv /data/MusicOther/ /media/brett/My\ Book/MusicOther/ --delete --prune-empty-dirs
```

######  Sync Music to SD card (delete files that no longer exist in source)
```bash
rsync -ahPv /data/Music/ /media/brett/android/Music/ --delete --prune-empty-dirs --ignore-existing
```

######  Backup my Recordings and sync my mp3 Recordings to all of my mp3 Music directories
```bash
rsync -ahPv /data/Recordings/ /media/brett/My\ Book/Recordings/ --delete --prune-empty-dirs
export MP3_SOURCE_DIR=/data/Recordings/mp3/Brett\ Tolbert/
rsync -ahPv "$MP3_SOURCE_DIR" /data/Music/Brett\ Tolbert/ --delete --prune-empty-dirs
rsync -ahPv "$MP3_SOURCE_DIR" /media/brett/My\ Book/Music/Brett\ Tolbert/ --delete --prune-empty-dirs
rsync -ahPv "$MP3_SOURCE_DIR" /media/android/Music/Brett\ Tolbert/ --delete --prune-empty-dirs
```

######  Find files that aren't music or album art and delete them
```bash
find "$MUSIC_DIR_LOCAL" -type f -not \( -iname "*.mp3" -o -iname "*.jpg" -o -iname "*.m4a" -o -iname "*.flac" \) -delete
```

######  Find files with the specified extensions and print them
```bash
find "$MUSIC_DIR_LOCAL" -type f \( -iname "*.flac" \) -print
```

######  Find files with the specified extensions and delete them
```bash
find "$MUSIC_DIR_LOCAL" -type f \( -iname "*.wav" -o -iname "*.wma" \) -delete
```

######  Find and delete empty directories
```bash
find "$MUSIC_DIR_LOCAL" -empty -type d -delete
```

######  Find and delete empty files
```bash
find "$MUSIC_DIR_LOCAL" -type f -size 0 -print -delete
```

######  Manually mount SD card
```bash
sudo umount /dev/sdc1
sudo mkdir -p /media/brett/android/
sudo mount -t vfat /dev/sdc1 /media/brett/android/ -o rw
```

######  Re-mount SD card as RW
```bash
sudo mount "$DIR_SDCARD" -o remount,rw
```

######  Count audio files (with specified extensions)
```bash
$ count_audio_files () { find "$1" -type f \( -iname "*.mp3" -o -iname "*.m4a" \) -print | wc -l; }

$ count_audio_files /data/Music
8041

$ count_audio_files /media/brett/My\ Book/Music
8041

$ count_audio_files /media/brett/android/Music
8041

```

######  Find duplicates and print them
```bash
rdfind -dryrun /data/Music
```

######  Find duplicates and delete them
```bash
rdfind -deleteduplicates true /data/Music
```
Example:
```bash
brett@brett-Z68XP-UD4:/data$ rdfind -deleteduplicates true /data/Music
Now scanning "/data/Music", found 12960 files.
Now have 12960 files in total.
Removed 0 files due to nonunique device and inode.
Total size is 54473875482 bytes or 51 GiB
Removed 8234 files due to unique sizes from list.4726 files left.
Now eliminating candidates based on first bytes:removed 290 files from list.4436 files left.
Now eliminating candidates based on last bytes:removed 37 files from list.4399 files left.
Now eliminating candidates based on sha1 checksum:removed 24 files from list.4375 files left.
It seems like you have 4375 files that are not unique
Totally, 989 MiB can be reduced.
Now making results file results.txt
Now deleting duplicates:
Deleted 2764 files.
```

######  Find SD card device ID
```bash
lsblk
```

######  Force unmount
```bash
sudo umount -l /dev/sdi1
```

######  Erase, repartition and reformat SD card (must unmount first)
Note: I didn't have much success with the commands below. I've had better luck formatting SD cards by running `Alt+F2` `gnome-disk` to launch the `Disks` utility.

Also if you get an error umounting e.g. *device in use*, try removing the USB card reader and re-inserting it. Also when the thing pops up after you insert the card, you have to click on it and open the directory, otherwise Budgie won't mount it.

```bash
sudo dd if=/dev/zero of=/dev/sdg bs=4096 status=progress
sudo parted /dev/sdg --script -- mklabel msdos
sudo parted /dev/sdg --script -- mkpart primary fat32 1MiB 100%
sudo mkfs.vfat -F32 /dev/sdg1
```

If mkfs failed with "device busy", try removing and using different SD card reader.

If mkfs fails with "failed whilst writing FAT", then SD card is likely going bad.

```bash
brett@brett-Z68XP-UD4:~$ sudo mkfs.vfat -F32 /dev/sdj1
mkfs.fat 4.2 (2021-01-31)
mkfs.vfat: failed whilst writing FAT
```

######  Inform kernel of partition table changes
```bash
$ sudo partprobe -s /dev/sdc
/dev/sdc: msdos partitions 1
```

######  Disable write protection
```bash
$ sudo hdparm -r0 /dev/sdc

/dev/sdc:
 setting readonly to 0 (off)
 readonly      =  0 (off)
```

###### Display partition and filesystem info
```bash
$ lsblk -f -m | grep sdc
sdc                                                                                                                       238.3G root  disk  brw-rw----
└─sdc1                                                                                                                    238.3G root  disk  brw-rw----
```

###### Print partition table
```bash
$ sudo parted /dev/sdh --script print
Model: Generic- SD/MMC (scsi)
Disk /dev/sdh: 256GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags: 

Number  Start   End    Size   Type     File system  Flags
 1      1049kB  256GB  256GB  primary               lba

```

###### Another way to print disk info
```bash
sudo fdisk -l
```

###### Something is auto-formatting the SD card:
```bash
$ sudo parted /dev/sdh --script print
Model: Generic STORAGE DEVICE (scsi)
Disk /dev/sdh: 256GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags: 

Number  Start   End    Size   Type     File system  Flags
 1      1049kB  256GB  256GB  primary  fat32        lba

```

###### ffmpeg audio conversion options
* `-c:a libmp3lame` - Use LAME mp3 encoder
* `-vn` - Disable video, to make sure no video (including album cover image) is included if the source would be a video file
* `-ar` - Set the audio sampling frequency. For output streams it is set by default to the frequency of the corresponding input stream. For input streams this option only makes sense for audio grabbing devices and raw demuxers and is mapped to the corresponding demuxer options.
* `-ac` - Set the number of audio channels. For output streams it is set by default to the number of input audio channels. For input streams this option only makes sense for audio grabbing devices and raw demuxers and is mapped to the 
corresponding demuxer options. So used here to make sure it is stereo (2 channels)
* `-q:a 2` - Convert audio bitrate to 192k VBR
* `-b:a 320k` - Convert audio bitrate to 320k CBR
* `-compression_level 8` - Use FLAC compression level `8` (default FLAC compression level is `5`, and that's probably what you should stick with)

###### Batch convert wav to mp3 (320k CBR) (drawback: wav filename case-sensitive)
```bash
shopt -s nocaseglob && shopt -s nocasematch && for f in *.wav; do ffmpeg -i "$f" -c:a libmp3lame -vn -ar 44100 -ac 2 -b:a 320k "${f/%wav/mp3}"; done
```

Note: `shopt -s nocaseglob && shopt -s nocasematch &&` makes it work even if the ".wav" file extension is uppercase (i.e. ".WAV")

###### Batch convert wav to flac
```bash
shopt -s nocaseglob && shopt -s nocasematch && for f in *.wav; do ffmpeg -i "$f" -c:a flac "${f/%wav/flac}"; done
```

###### Batch convert wav to mp3 (320k CBR) and flac
```bash
shopt -s nocaseglob && shopt -s nocasematch && for f in *.wav; do ffmpeg -i "$f" -c:a libmp3lame -vn -ar 44100 -ac 2 -b:a 320k "${f/%wav/mp3}" -c:a flac "${f/%wav/flac}"; done
```

###### Batch convert wav to mp3 (320k CBR) and ogg
```bash
shopt -s nocaseglob && shopt -s nocasematch && for f in *.wav; do ffmpeg -i "$f" -c:a libmp3lame -vn -ar 44100 -ac 2 -b:a 320k "${f/%wav/mp3}" -c:a libvorbis -q:a 4 "${f/%wav/ogg}"; done
```

###### id3v2 command
There are two major versions of ID3 tags: ID3v1 and ID3v2. ID3v2 has many features such as custom genre tags. Some older tools like `mp3info` can´t read ID3v2 tags, and `id3v2` can't read ID3v2.4 tags, so I reccommend `ffprobe` Demo:
```bash
$ find /data/Music -type f \( -iname "*.mp3" -o -iname "*.m4a" \) -exec ffprobe {} \; 2>&1 | egrep "genre" | sort | uniq -c | sort -rn -k1.4,7
   1182     genre           : Indie Rock
    915     genre           : Classic Rock
    586     genre           : Classic Prog
    475     genre           : Alternative Rock
    426     genre           : Funk Rock
    330     genre           : Country
    326     genre           : Post-Hardcore
    214     genre           : Electronica
    206     genre           : Classical
    204     genre           : Indie Folk
    173     genre           : Electropop
    173     genre           : Brett Tolbert
    158     genre           : Alternative Metal
    149     genre           : Post-Punk
    145     genre           : Pop Rock
    138     genre           : Emo / Pop-Rock
    127     genre           : Britpop
    124     genre           : New Wave français
    108     genre           : Post-Grunge
    100     genre           : Electronic (Instrumental)
     89     genre           : Hip-Hop
     83     genre           : Post-Punk Revival
     79     genre           : Folk Punk
     78     genre           : Desert Rock
     76     genre           : Other
     76     genre           : Funk (Instrumental)
     72     genre           : Grunge
     69     genre           : Pop-Punk
     65     genre           : Folk
     61     genre           : Rap Rock
     56     genre           : Southern Rock
     55     genre           : Post-Industrial
     54     genre           : Neo-Psychedelic Rock
     51     genre           : Pop
     46     genre           : Progressive Pop
     44     genre           : Punk français
     42     genre           : Soft Rock
     41     genre           : Post-Rock
     41     genre           : Electronic w/ vocals
     35     genre           : Indie Pop
     26     genre           : Punk
     26     genre           : Psychedelic Rock
     26     genre           : Industrial Metal
     26     genre           : Industrial
     24     genre           : Soundtrack
     22     genre           : Progressive Metal
     21     genre           : Punk Rock
     21     genre           : Math Rock
     20     genre           : Pop française
     17     genre           : Reggae
     17     genre           : Metal
     16     genre           : Heavy Metal
     15     genre           : Blues
     14     genre           : Indie
     13     genre           : Industrial Rock
     13     genre           : Dub
     12     genre           : Dream Pop
     12     genre           : Blues Rock
     11     genre           : R&B
     11     genre           : New Wave
     10     genre           : Reggae Rock
     10     genre           : Chillwave
      9     genre           : Rock français
      8     genre           : Experimental
      7     genre           : Progressive Rock
      7     genre           : Post-Black Metal
      6     genre           : Funk Metal
      5     genre           : Folk Rock
      5     genre           : Backing Tracks
      4     genre           : Post-Metal
      3     genre           : Soul
      3     genre           : Gospel
      3     genre           : genre
      3     genre           : Folk Pop
      3     genre           : Drumline
      3     genre           : Comedy
      3     genre           : Bluegrass
      2     genre           : World
      2     genre           : Ska Punk
      2     genre           : Nu Metal français
      2     genre           : Nu Metal
      2     genre           : Metalcore
      2     genre           : Hip-Hop français
      1     genre           : Surf Rock
      1     genre           : Sports
      1     genre           : Miscellaneous
      1     genre           : Jazz
      1     genre           : Heartland Rock
      1     genre           : Grindcore
      1     genre           : Glam Rock
      1     genre           : General Country
```

# USB troubleshooting reset high-speed USB device number 5 using ehci-pci error

Probable cause: low voltage issue
Solution: Use powered USB hub
Trick is to use `dmesg -w` to show the output of `dmesg` in realtime (similar to `tail -f`) and then you can observe what happens when you connect or disconnect USB devices to determine the device numbers.

```bash
$ sudo dmesg -w
[473947.435688] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[473980.203503] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474012.975195] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474045.738940] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474078.506705] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474111.274481] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474144.042264] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474176.814045] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474209.577864] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474242.345677] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474275.113493] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474307.881315] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474340.649146] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474373.416965] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474406.184794] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474438.952622] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474471.720452] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474504.488342] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474537.256270] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci
[474566.152201] usb 2-1.8: new high-speed USB device number 9 using ehci-pci
[474566.264632] usb 2-1.8: New USB device found, idVendor=0409, idProduct=005a, bcdDevice= 1.00
[474566.264640] usb 2-1.8: New USB device strings: Mfr=0, Product=0, SerialNumber=0
[474566.264998] hub 2-1.8:1.0: USB hub found
[474566.265076] hub 2-1.8:1.0: 4 ports detected
[474570.024189] usb 2-1.5: reset high-speed USB device number 5 using ehci-pci

```

- The `5` in `usb 2-1.5` indicates it's USB device number 5 (assuming this is on the front of my PC)
- The `8` in `usb 2-1.8` indicates it's USB device number 8 (one of the red ports on the back of my PC)
- Device `usb 3-1` is one of the blue ports on the front panel
- Device 8 is one of the USB ports on the top of the front-panel.

> Literally the message says that Linux USB stack has issued "USB_RESET" to your particular device (devices #19 and #20, whatever they are). The error seems to occur once per 10-30 seconds. After reset, the log should have fresh enumeration messages, since USB reset will force the connected device into "default state". Looks like verbosity of your log is very reduced.

> Resetting a USB device in the middle of operation is a pretty drastic situation. The controller resorts to this "port" reset if it encounters "transaction error". Transaction error occurs when the link does not complete all required phases of USB transaction, or has a CRC error. In normal USB the EHCI controller will automatically re-try the failing transaction (typical maximum 3 times), and then will set an XACT_ERROR interrupt. Statistically, by error theory, if a link does not respond properly to three attempts in a row, there is something wrong with the particular USB segment, mostly electrically. So the transaction error is considered as fatal, and software tries to recover the link. If tree-four attempts to recover the link fail, the host considers this port as dead, and quits.

> In Linux however, someone has decided that 3 theoretical attempts is not enough, and Linux software performs additional 32 (thirty-two) attempts, making it 96 (!!!) total. If the hardware link happens to be electrically marginal, the 96 attempts might succeed in 99.99% of the time. Linux software gurus claim that this helps to improve operability of questionable devices/cables. In essence, this technique hides a serious problem with this particular USB connection, which does not help users in long run.

> The problem could be in marginal voltage (VBUS) supply to the drives, or VBUS glitches, or signal degradation on signal wires. I would try extremely short high-quality certified cables first, and check if the statistics of error changes. 


```
brett@brett-Z68XP-UD4:~$ lsusb
Bus 002 Device 009: ID 0409:005a NEC Corp. HighSpeed Hub
Bus 002 Device 005: ID 058f:6364 Alcor Micro Corp. AU6477 Card Reader Controller
Bus 002 Device 011: ID 7392:7811 Edimax Technology Co., Ltd EW-7811Un 802.11n Wireless Adapter [Realtek RTL8188CUS]
Bus 002 Device 010: ID 046d:c52f Logitech, Inc. Unifying Receiver
Bus 002 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 006 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 005 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 004: ID 046d:c33b Logitech, Inc. K840 Mechanical Corded Keyboard
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

Oh, so `usb 2-1.5` is actually the card reader?

`Bus 002 Device 005: ID 058f:6364 Alcor Micro Corp. AU6477 Card Reader Controller`

