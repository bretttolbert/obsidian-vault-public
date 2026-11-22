# VLC commands

###### RTP stream from video

```bash
cvlc -vvv video.mp4 --loop --sout '#transcode{vcodec=h264,vb=800}:rtp{dst=127.0.0.1,port=60010,mux=ts,name=Channel1}' --sout-keep &
```

###### RTSP Restream an RTP stream

- `rtp://127.0.0.1:60010` = stream URI
- `127.0.0.1` = restream IP 
- `60010` = RTP input stream port
- `70010` = RTSP re-stream port
- `rtsp://127.0.0.1:70010/Channel1.sdp` = SDP URI for RTSP re-stream

```bash
cvlc -vvv rtp://127.0.0.1:60010 --rtsp-host 127.0.0.1 --sout '#rtp{name=Channel1,port=60010,sdp=rtsp://127.0.0.1:70010/Channel1.sdp}' &
```
