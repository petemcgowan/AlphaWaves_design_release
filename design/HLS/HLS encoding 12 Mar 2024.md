General: Run ffmpeg -i on any video to find out what kinds of streams are in it.  

TODO: Update the stream playlist files to have the directory in them (after you've created)

100k 360x640   only have this if it's 540x960 file
200k 540x960
400k 720x1280
800k 1080x1920

DONE TWO - RainInACar   
----------
ffmpeg -i RainInACar.mp4 -c:v libx264 -crf 20 -preset veryslow -profile:v baseline -r 23.976 \
-map 0:v:0 -b:v:0 200k -s:v:0 360x640 \
-map 0:v:0 -b:v:1 800k -s:v:1 540x960 \
-f hls -hls_time 4 -hls_playlist_type vod -hls_segment_filename 'stream_%v/data%06d.ts' \
-var_stream_map "v:0 v:1" \
-master_pl_name master.m3u8 stream_%v.m3u8


DONE  TWO  - RainFallingOnLeaves (1080x1920)
----------
ffmpeg -i RainFallingOnLeaves.mp4 -c:v libx264 -crf 21 -preset veryslow -profile:v baseline -r 23.976 \
-map 0:v:0 -b:v:0 500k -s:v:0 540x960 \
-map 0:v:0 -b:v:1 800k -s:v:1 720x1280 \
-map 0:v:0 -b:v:2 1300k -s:v:2 1080x1920 \
-f hls -hls_time 4 -hls_playlist_type vod -hls_segment_filename 'stream_%v/data%06d.ts' \
-var_stream_map "v:0 v:1 v:2" \
-master_pl_name master.m3u8 stream_%v.m3u8



-------------------------------------------
DONE TWO - blueSplashes  (1920x1080  59.96 fp)
--------------


ffmpeg -i blueSplashes.mp4 -c:v libx264 -crf 26 -g 37 -preset veryslow -profile:v baseline -r 23.976 \
-map 0:v:0 -b:v:0 500k -s:v:0 540x960 \
-map 0:v:0 -b:v:1 800k -s:v:1 720x1280 \
-map 0:v:0 -b:v:2 1300k -s:v:2 1080x1920 \
-f hls -hls_time 4 -hls_playlist_type vod -hls_segment_filename 'stream_%v/data%06d.ts' \
-var_stream_map "v:0 v:1 v:2" \
-master_pl_name master.m3u8 stream_%v.m3u8



-------------------------------------------
DONE - RainInACarAltHD (1920x1080)
----------

ffmpeg -i RainInACarAltHD.mp4 -c:v libx264 -crf 22 -g 48 -preset veryslow -profile:v baseline -r 23.976 \
-map 0:v:0 -b:v:0 500k -s:v:0 540x960 \
-map 0:v:0 -b:v:1 800k -s:v:1 720x1280 \
-map 0:v:0 -b:v:2 1300k -s:v:2 1080x1920 \
-f hls -hls_time 2 -hls_playlist_type vod -hls_segment_filename 'stream_%v/data%06d.ts' \
-var_stream_map "v:0 v:1 v:2" \
-master_pl_name master.m3u8 stream_%v.m3u8



DONE - rainInPorchOverlookingForest (1920x1080)
----------

ffmpeg -i rainInPorchOverlookingForest.mp4 -c:v libx264 -g 52 -crf 26 -preset veryslow -profile:v baseline -r 23.976 \
-map 0:v:0 -b:v:0 200k -s:v:0 540x960 \
-map 0:v:0 -b:v:1 400k -s:v:1 720x1280 \
-map 0:v:0 -b:v:2 800k -s:v:2 1080x1920 \
-f hls -hls_time 4 -hls_playlist_type vod -hls_segment_filename 'stream_%v/data%06d.ts' \
-var_stream_map "v:0 v:1 v:2" \
-master_pl_name master.m3u8 stream_%v.m3u8


DONE - rainPouringDown
----------

ffmpeg -i rainPouringDown.mp4 -c:v libx264 -crf 25  -g 48 -preset veryslow -profile:v baseline -r 23.976 \
-map 0:v:0 -b:v:0 200k -s:v:0 540x960 \
-map 0:v:0 -b:v:1 400k -s:v:1 720x1280 \
-map 0:v:0 -b:v:2 800k -s:v:2 1080x1920 \
-f hls -hls_time 4 -hls_playlist_type vod -hls_segment_filename 'stream_%v/data%06d.ts' \
-var_stream_map "v:0 v:1 v:2" \
-master_pl_name master.m3u8 stream_%v.m3u8




----------------------
Informational

Possible presets: ultrafast superfast veryfast faster fast medium slow slower veryslow placebo







------------------------------
ffmpeg -i RainInACar.mp4 \
-c:v libx264 -crf 20 -preset veryslow -profile:v baseline -r 23.976 \
-map 0:v:0 -s:v:0 270x480 \
-map 0:v:0 -s:v:1 360x640 \
-map 0:v:0 -s:v:2 540x960 \
-map 0:v:0 -s:v:3 720x1280 \
-map 0:v:0 -s:v:4 1080x1920 \
-f hls -hls_time 4 -hls_playlist_type vod \
-hls_segment_filename './stream%v/data%06d.ts' \
-var_stream_map "v:0 v:1 v:2 v:3 v:4" \
-master_pl_name master.m3u8 \
-master_pl_publish_rate 100 \
-hls_base_url "stream%v/" \
./stream%v.m3u8



ffmpeg -i RainInACar.mp4 \
-c:v libx264 -crf 18 -preset veryslow -profile:v baseline -r 23.976 \
-map 0:v:0 -s:v:0 270x480 \
-map 0:v:0 -s:v:1 360x640 \
-map 0:v:0 -s:v:2 540x960 \
-map 0:v:0 -s:v:3 720x1280 \
-map 0:v:0 -s:v:4 1080x1920 \
-f hls -hls_time 4 -hls_playlist_type vod \
-hls_segment_filename './stream%v/data%06d.ts' \
-var_stream_map "v:0 v:1 v:2 v:3 v:4" \
-master_pl_name master.m3u8 \
-hls_base_url "stream%v/" \
./stream%v.m3u8






ffmpeg -i RainInACar.mp4 \
-c:v libx264 -crf 20 -preset veryslow -profile:v baseline -r 23.976 \
-map 0:v:0 -s:v:0 270x480 \
-map 0:v:0 -s:v:1 360x640 \
-map 0:v:0 -s:v:2 540x960 \
-map 0:v:0 -s:v:3 720x1280 \
-map 0:v:0 -s:v:4 1080x1920 \
-f hls -hls_time 4 -hls_playlist_type vod \
-hls_segment_filename './stream%v/data%06d.ts' \
-var_stream_map "v:0 v:1 v:2 v:3 v:4" \
-master_pl_name master.m3u8 \
-hls_base_url "stream%v/" \
./stream%v.m3u8





ffmpeg -i RainInACar.mp4 \
  -c:v libx264 -crf 23 -preset slowest -profile:v baseline \  -r 23.976  -map 0:v:0 -s:v:2 540x960  \  -map 0:v:0 -s:v:3 720x1280  \  -map 0:v:0 -s:v:4 1080x1920  \   -f hls -hls_time 4 -hls_playlist_type vod -hls_segment_filename 'stream%v/data%06d.ts' \  -var_stream_map "v:0 v:1 v:2 v:3 v:4" \  -master_pl_name master.m3u8 stream%v.m3u8 


ffmpeg -i RainInACar.mp4 -c:v libx264 -crf 25 -preset veryslow -profile:v baseline -r 23.976 -map 0:v:0 -s:v:2 540x960 -map 0:v:0 -s:v:3 720x1280 -map 0:v:0 -s:v:4 1080x1920 -f hls -hls_time 4 -hls_playlist_type vod -hls_segment_filename './stream%v/data%06d.ts' -var_stream_map "v:0 v:1 v:2 v:3 v:4" -master_pl_name ./master.m3u8 ./stream%v.m3u8






ffmpeg -i RainInACar.mp4 -c:v libx264 -crf 25 -preset veryslow -profile:v baseline -r 23.976 -f hls -hls_time 4 -hls_playlist_type vod -hls_segment_filename './stream0/data%06d.ts' -master_pl_name ./master.m3u8


This one works?
ffmpeg -i RainInACar.mp4 -c:v libx264 -crf 23 -preset slower -profile:v baseline -r 23.976 -map 0:v:0 -s:v:0 270x480 -map 0:v:0 -s:v:1 360x640 -map 0:v:0 -s:v:2 540x960 -map 0:v:0 -s:v:3 720x1280 -map 0:v:0 -s:v:4 1080x1920 -f hls -hls_time 4 -hls_playlist_type vod -hls_segment_filename './stream%v/data%06d.ts' -var_stream_map "v:0 v:1 v:2 v:3 v:4" -master_pl_name ./master.m3u8 ./stream%v.m3u8 

Trying this:
ffmpeg -i RainInACar.mp4 -c:v libx264 -crf 25 -preset veryslow -profile:v baseline -r 23.976 -map 0:v:0 -s:v:0 270x480 -map 0:v:0 -s:v:1 360x640 -map 0:v:0 -s:v:2 540x960 -map 0:v:0 -s:v:3 720x1280 -map 0:v:0 -s:v:4 1080x1920 -f hls -hls_time 4 -hls_playlist_type vod -hls_segment_filename './stream%v/data%06d.ts' -var_stream_map "v:0 v:1 v:2 v:3 v:4" -master_pl_name ./master.m3u8 ./stream%v.m3u8 




I have a HLS encoding command that creates files almost how we want them but seems to have some issues can you help modify it so it create things perhaps more how we need them?  Here's the semi-working command: ffmpeg -i RainInACar.mp4 -c:v libx264 -crf 25 -preset veryslow -profile:v baseline -r 23.976 -map 0:v:0 -s:v:0 270x480 -map 0:v:0 -s:v:1 360x640 -map 0:v:0 -s:v:2 540x960 -map 0:v:0 -s:v:3 720x1280 -map 0:v:0 -s:v:4 1080x1920 -f hls -hls_time 4 -hls_playlist_type vod -hls_segment_filename './stream%v/data%06d.ts' -var_stream_map "v:0 v:1 v:2 v:3 v:4" -master_pl_name ./master.m3u8 ./stream%v.m3u8


It's creating directories and encoding files .  But something I'm noticing with this approach is that it creates the files but it doesn't seem to create the master file very well?  It only contains this text, which feels like it's missing the necessary directives?            #EXTM3U
#EXT-X-VERSION:3
                 I also notice that the stream m3u8 files are missing the necessary sub-directory, here's an example of what one that is produced:   #EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:10
#EXT-X-MEDIA-SEQUENCE:0
#EXT-X-PLAYLIST-TYPE:VOD
#EXTINF:10.427089,
data000000.ts
#EXTINF:10.427100,
data000001.ts
#EXTINF:9.218156,
data000002.ts
#EXT-X-ENDLIST