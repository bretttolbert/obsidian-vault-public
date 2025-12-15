# ffprobe

###### `ffprobe` vs `id3v2` vs `mp3info`
- There are two major versions of ID3 tags: ID3v1 and ID3v2
- ID3v1 is limited to a limited number of predefined genre tags
- ID3v2 adds many features such as custom genre tags
- `mp3info` can´t read ID3v2 tags
- `id3v2` can't read ID3v2.4 tags
- `ffprobe` can read both


##### `ffprobe` demo:
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


###### ffprobe json output
```bash
brett@timebox:~/Git/timebox/timebox $ ffprobe -v quiet -print_format json -show_format -show_streams '/home/brett/Music/Cream/The Very Best Of Cream/15 Those Were The Days.mp3'
{
    "streams": [
        {
            "index": 0,
            "codec_name": "mp3",
            "codec_long_name": "MP3 (MPEG audio layer 3)",
            "codec_type": "audio",
            "codec_time_base": "1/44100",
            "codec_tag_string": "[0][0][0][0]",
            "codec_tag": "0x0000",
            "sample_fmt": "fltp",
            "sample_rate": "44100",
            "channels": 2,
            "channel_layout": "stereo",
            "bits_per_sample": 0,
            "r_frame_rate": "0/0",
            "avg_frame_rate": "0/0",
            "time_base": "1/14112000",
            "start_pts": 353600,
            "start_time": "0.025057",
            "duration_ts": 2500485120,
            "duration": "177.188571",
            "bit_rate": "320000",
            "disposition": {
                "default": 0,
                "dub": 0,
                "original": 0,
                "comment": 0,
                "lyrics": 0,
                "karaoke": 0,
                "forced": 0,
                "hearing_impaired": 0,
                "visual_impaired": 0,
                "clean_effects": 0,
                "attached_pic": 0,
                "timed_thumbnails": 0
            },
            "tags": {
                "encoder": "LAME3.98r"
            }
        }
    ],
    "format": {
        "filename": "/home/brett/Music/Cream/The Very Best Of Cream/15 Those Were The Days.mp3",
        "nb_streams": 1,
        "nb_programs": 0,
        "format_name": "mp3",
        "format_long_name": "MP2/3 (MPEG audio layer 2/3)",
        "start_time": "0.025057",
        "duration": "177.188571",
        "size": "7090304",
        "bit_rate": "320124",
        "probe_score": 51,
        "tags": {
            "album": "The Very Best Of Cream",
            "artist": "Cream",
            "encoder": "Lame3.98",
            "genre": "Classic Rock",
            "title": "Those Were The Days",
            "track": "15",
            "publisher": "Polydor",
            "album_artist": "Cream",
            "composer": "Gene Raskin/Ginger Baker/Mike Taylor",
            "date": "1969",
            "id3v2_priv.WM/UniqueFileIdentifier": "A\\x00M\\x00G\\x00a\\x00_\\x00i\\x00d\\x00=\\x00R\\x00 \\x00 \\x00 \\x002\\x001\\x002\\x009\\x005\\x004\\x00;\\x00A\\x00M\\x00G\\x00p\\x00_\\x00i\\x00d\\x00=\\x00P\\x00 \\x00 \\x00 \\x00 \\x00 \\x003\\x009\\x008\\x003\\x00;\\x00A\\x00M\\x00G\\x00t\\x00_\\x00i\\x00d\\x00=\\x00T\\x00 \\x00 \\x002\\x005\\x000\\x006\\x003\\x003\\x006\\x00\\x00\\x00",
            "id3v2_priv.WM/WMCollectionGroupID": "\\xefR\\xe4h\\xd9\\xd1pL\\x82\\x13\\xb5\\xcb\\x08\\x9f>\\x8f",
            "id3v2_priv.WM/WMCollectionID": "\\xefR\\xe4h\\xd9\\xd1pL\\x82\\x13\\xb5\\xcb\\x08\\x9f>\\x8f",
            "id3v2_priv.WM/WMContentID": "\\x14W\\xee\\x0d\\x9f\\xf7LM\\xba\\x1f\\xea\\xe5{\\xf5\\xfaC",
            "id3v2_priv.WM/Provider": "A\\x00M\\x00G\\x00\\x00\\x00",
            "id3v2_priv.WM/MediaClassPrimaryID": "\\xbc}`\\xd1#\\xe3\\xe2K\\x86\\xa1H\\xa4*(D\\x1e",
            "id3v2_priv.WM/MediaClassSecondaryID": "\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00"
        }
    }
}
```