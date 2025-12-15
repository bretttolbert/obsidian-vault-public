# Setting the Default Soundcard (ALSA)

Find your desired card with:

```bash
   cat /proc/asound/cards
```

and then create /etc/asound.conf with following:

```bash
   defaults.pcm.card 1
   defaults.ctl.card 1
```

Replace "1" with number of your card determined above. 
