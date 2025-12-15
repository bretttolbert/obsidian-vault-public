# yt-dlp


## Download YouTube audio and convert to mp3

Note: Use `-S res,ext:mp4:m4a` instead of the old `-f bestaudio`

```bash
yt-dlp -S res,ext:mp4:m4a --extract-audio --audio-format mp3 --audio-quality 0 --embed-metadata --parse-metadata "playlist_index:%(track_number)s" --add-metadata -o "%(track_number)s - %(title)s.%(ext)s" --cookies-from-browser firefox $1
```
