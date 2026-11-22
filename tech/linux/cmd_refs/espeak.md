# espeak

###### speak text - output to speaker
```bash
espeak -v en -a 100 -p 0 -s 125 "I brought you into a fertile land to eat its fruit and rich produce. But you came and defiled my land and made my inheritance detestable."
```

###### speak text - output to WAV file
```bash
espeak -v en -a 100 -p 0 -s 125 -f input.txt --stdout > out.wav
```

###### speak text - output to MP3 file
```bash
espeak -v en -a 100 -p 0 -s 125 -f input.txt --stdout | ffmpeg -i - -ar 44100 -ac 2 -ab 192k -f mp3 out.mp3
```

