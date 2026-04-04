
Note: You still have to input the "stream_" directories into each stream playlist, as it doesn't put them in there.  

Restart  to enforce copying up files down and then up the docker container:
docker-compose up --build

Target file (open in VLC to see if it works ok): 
http://ec2-52-23-111-225.compute-1.amazonaws.com:8080/rainPouringDown/master.m3u8


TODO: Bizarre app behaviour may be the dynamic IP?
TODO: Don't forget rest of file sets you need to do!
TODO: This process needs to be modded for rainInaCar (?) as it's "560" res not 1080, so it's slightly different.  
TODO: Watch rate, rainPouringDown was already 24, so didn't need conversion


rainPour
NEW WAY: 
https://ottverse.com/hls-packaging-using-ffmpeg-live-vod/



WORKS
ffmpeg -i rainPouringDown.mp4 \
-filter_complex \
"[0:v]split=2[v1][v2]; \
[v1]copy[v1out]; [v2]scale=w=720:h=1280[v2out]" \
-map "[v1out]" -c:v:0 libx264 -x264-params "nal-hrd=cbr:force-cfr=1" -b:v:0 4M -maxrate:v:0 4M -minrate:v:0 4M -bufsize:v:0 7M -preset slow -g 48 -sc_threshold 0 -keyint_min 48 \
-map "[v2out]" -c:v:1 libx264 -x264-params "nal-hrd=cbr:force-cfr=1" -b:v:1 2M -maxrate:v:1 2M -minrate:v:1 2M -bufsize:v:1 5M -preset slow -g 48 -sc_threshold 0 -keyint_min 48 \
-r 24 \
-f hls \
-hls_time 2 \
-hls_playlist_type vod \
-hls_flags independent_segments \
-hls_segment_type mpegts \
-hls_segment_filename stream_%v/data%02d.ts \
-master_pl_name master.m3u8 \
-var_stream_map "v:0 v:1" stream_%v.m3u8



KEEPER SAFE:   (this one works, I'm not adjusting cause it's still picking the smallest rate)
-------------
ffmpeg -i rainPouringDown.mp4 \
-filter_complex \
"[0:v]split=3[v1][v2][v3]; \
[v1]copy[v1out]; [v2]scale=w=720:h=1280[v2out]; [v3]scale=w=360:h=640[v3out]" \
-map "[v1out]" -c:v:0 libx264 -x264-params "nal-hrd=cbr:force-cfr=1" -b:v:0 5M -maxrate:v:0 5M -minrate:v:0 5M -bufsize:v:0 10M -preset slow -g 48 -sc_threshold 0 -keyint_min 48 \
-map "[v2out]" -c:v:1 libx264 -x264-params "nal-hrd=cbr:force-cfr=1" -b:v:1 3M -maxrate:v:1 3M -minrate:v:1 3M -bufsize:v:1 3M -preset slow -g 48 -sc_threshold 0 -keyint_min 48 \
-map "[v3out]" -c:v:2 libx264 -x264-params "nal-hrd=cbr:force-cfr=1" -b:v:2 1M -maxrate:v:2 1M -minrate:v:2 1M -bufsize:v:2 1M -preset slow -g 48 -sc_threshold 0 -keyint_min 48 \
-f hls \
-hls_time 2 \
-hls_playlist_type vod \
-hls_flags independent_segments \
-hls_segment_type mpegts \
-hls_segment_filename stream_%v/data%02d.ts \
-master_pl_name master.m3u8 \
-var_stream_map "v:0 v:1 v:2" stream_%v.m3u8

