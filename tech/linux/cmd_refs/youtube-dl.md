# youtube-dl

###### Extract audio with youtube-dl

```bash
youtube-dl -x --audio-format mp3 --audio-quality 0 https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

- https://github.com/ytdl-org/youtube-dl

## Download Options:
```
-r, --limit-rate RATE                Maximum download rate in bytes per
                                     second (e.g. 50K or 4.2M)
-R, --retries RETRIES                Number of retries (default is 10), or
                                     "infinite".
--fragment-retries RETRIES           Number of retries for a fragment
                                     (default is 10), or "infinite" (DASH,
                                     hlsnative and ISM)
--skip-unavailable-fragments         Skip unavailable fragments (DASH,
                                     hlsnative and ISM)
--abort-on-unavailable-fragment      Abort downloading when some fragment is
                                     not available
--keep-fragments                     Keep downloaded fragments on disk after
                                     downloading is finished; fragments are
                                     erased by default
--buffer-size SIZE                   Size of download buffer (e.g. 1024 or
                                     16K) (default is 1024)
--no-resize-buffer                   Do not automatically adjust the buffer
                                     size. By default, the buffer size is
                                     automatically resized from an initial
                                     value of SIZE.
--http-chunk-size SIZE               Size of a chunk for chunk-based HTTP
                                     downloading (e.g. 10485760 or 10M)
                                     (default is disabled). May be useful
                                     for bypassing bandwidth throttling
                                     imposed by a webserver (experimental)
--playlist-reverse                   Download playlist videos in reverse
                                     order
--playlist-random                    Download playlist videos in random
                                     order
--xattr-set-filesize                 Set file xattribute ytdl.filesize with
                                     expected file size
--hls-prefer-native                  Use the native HLS downloader instead
                                     of ffmpeg
--hls-prefer-ffmpeg                  Use ffmpeg instead of the native HLS
                                     downloader
--hls-use-mpegts                     Use the mpegts container for HLS
                                     videos, allowing to play the video
                                     while downloading (some players may not
                                     be able to play it)
--external-downloader COMMAND        Use the specified external downloader.
                                     Currently supports aria2c,avconv,axel,c
                                     url,ffmpeg,httpie,wget
--external-downloader-args ARGS      Give these arguments to the external
                                     downloader
```

## Post-processing Options:
```
-x, --extract-audio                  Convert video files to audio-only files
                                     (requires ffmpeg/avconv and
                                     ffprobe/avprobe)
--audio-format FORMAT                Specify audio format: "best", "aac",
                                     "flac", "mp3", "m4a", "opus", "vorbis",
                                     or "wav"; "best" by default; No effect
                                     without -x
--audio-quality QUALITY              Specify ffmpeg/avconv audio quality,
                                     insert a value between 0 (better) and 9
                                     (worse) for VBR or a specific bitrate
                                     like 128K (default 5)
--recode-video FORMAT                Encode the video to another format if
                                     necessary (currently supported:
                                     mp4|flv|ogg|webm|mkv|avi)
--postprocessor-args ARGS            Give these arguments to the
                                     postprocessor
-k, --keep-video                     Keep the video file on disk after the
                                     post-processing; the video is erased by
                                     default
--no-post-overwrites                 Do not overwrite post-processed files;
                                     the post-processed files are
                                     overwritten by default
--embed-subs                         Embed subtitles in the video (only for
                                     mp4, webm and mkv videos)
--embed-thumbnail                    Embed thumbnail in the audio as cover
                                     art
--add-metadata                       Write metadata to the video file
--metadata-from-title FORMAT         Parse additional metadata like song
                                     title / artist from the video title.
                                     The format syntax is the same as
                                     --output. Regular expression with named
                                     capture groups may also be used. The
                                     parsed parameters replace existing
                                     values. Example: --metadata-from-title
                                     "%(artist)s - %(title)s" matches a
                                     title like "Coldplay - Paradise".
                                     Example (regex): --metadata-from-title
                                     "(?P<artist>.+?) - (?P<title>.+)"
--xattrs                             Write metadata to the video file's
                                     xattrs (using dublin core and xdg
                                     standards)
--fixup POLICY                       Automatically correct known faults of
                                     the file. One of never (do nothing),
                                     warn (only emit a warning),
                                     detect_or_warn (the default; fix file
                                     if we can, warn otherwise)
--prefer-avconv                      Prefer avconv over ffmpeg for running
                                     the postprocessors
--prefer-ffmpeg                      Prefer ffmpeg over avconv for running
                                     the postprocessors (default)
--ffmpeg-location PATH               Location of the ffmpeg/avconv binary;
                                     either the path to the binary or its
                                     containing directory.
--exec CMD                           Execute a command on the file after
                                     downloading and post-processing,
                                     similar to find's -exec syntax.
                                     Example: --exec 'adb push {}
                                     /sdcard/Music/ && rm {}'
--convert-subs FORMAT                Convert the subtitles to other format
                                     (currently supported: srt|ass|vtt|lrc)
 ```