# sox 

SoX is a command-line audio processing tool, particularly suited to making quick, simple edits and to batch processing.

## History

SoX was created in July 1991 by Lance Norskog and posted to the Usenet group alt.sources as Aural eXchange: Sound sample translator. With the second release (in November the same year) it was renamed Sound Exchange. 

## Features

Some of SoX's features are:

- Cross-platform (Windows, Linux, Solaris, OS X, et al.)
- Reading and writing Au, WAV, AIFF, MP3 (via an external LAME MP3 encoder), Ogg Vorbis, FLAC and other audio file formats
- Recording and playing audio (on many systems); playing via URL (internet file or stream)
- Editing via concatenate, trim, pad, repeat, reverse, volume, fade, splice, normalise
- Processing via chorus, flanger, echo, phaser, compressor, delay, filter (high-pass, low-pass, shelving, etc.)
- Adjustment of speed (pitch and tempo), pitch (without tempo), tempo (without pitch), and sample rate
- Noise removal using frequency profiling, implemented since December 2004
- Silent passage removal, implemented since September 2001
- Simple audio synthesis
- Multi-file & multi-track mixing
- Multi-file merging (e.g., 2 mono to 1 stereo)
- **Statistical analysis; spectrogram analysis**

###### Install sox

```bash
sudo apt install -y sox libsox-fmt-mp3
```

###### Use sox to calculate average volume of mp3

```bash
$ sox Faith\ No\ More\ -\ Midlife\ Crisis.mp3 -n stat
Samples read:          23279596
Length (seconds):    263.940998
Scaled by:         2147483647.0
Maximum amplitude:     1.000000
Minimum amplitude:    -1.000000
Midline amplitude:    -0.000000
Mean    norm:          0.158768
Mean    amplitude:    -0.000064
RMS     amplitude:     0.218801
Maximum delta:         1.151079
Minimum delta:         0.000000
Mean    delta:         0.103471
RMS     delta:         0.144737
Rough   frequency:         4642
Volume adjustment:        1.000

```
