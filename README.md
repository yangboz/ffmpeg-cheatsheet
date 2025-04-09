Here’s your cleaned and corrected Markdown content, properly formatted and organized for clarity and consistency:

⸻

FFMPEG Cheatsheet

For single image processing, check: ImageMagick Cheatsheet

⸻

Want to improve this cheat sheet? See the Contributing section!

Table of Contents
	•	Why FFMPEG?
	•	Prerequisites
	•	Installation
	•	Best Practices
	•	Tools
	•	Contributing
	•	References
	•	Known Issues

⸻

Why FFMPEG?

FFmpeg is the leading multimedia framework, able to decode, encode, transcode, mux, demux, stream, filter, and play nearly anything ever created. It supports the most obscure ancient formats up to the latest cutting-edge standards.

It is highly portable—FFmpeg compiles, runs, and passes tests across Linux, macOS, Windows, BSDs, Solaris, etc.

A complete, cross-platform solution to record, convert, and stream audio and video.
TL;NR: Converting video and audio has never been so easy.

⸻

Prerequisites

See: FFmpeg Documentation

Video formats: mp4, avi, mpeg, flv, …

Codecs:
[Too Long; Not Read]

⸻

Installation

Official download: FFmpeg Downloads

Linux

apt-get install ffmpeg

yum install ffmpeg

macOS

brew install ffmpeg

Windows

Visit: FFmpeg Windows Builds

⸻

Cheatsheet

Syntax

ffmpeg [global_options] {[input_file_options] -i input_url} ... {[output_file_options] output_url} ...

Get Info

ffmpeg -i input.mp4

Convert Formats

MP4 to AVI

ffmpeg -i input.mp4 output.avi

GIF to MP4

ffmpeg -i animated.gif -movflags faststart -pix_fmt yuv420p -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" video.mp4

WEBM to MP4

ffmpeg -i movie.webm movie.mp4

Image Operations

Extract images from video

ffmpeg -i video.mpg image-%04d.jpg

PNGs to video

ffmpeg -framerate 30 -pattern_type glob -i '*.png' -c:v libx264 -pix_fmt yuv420p out.mp4

JPGs to video with video filter

ffmpeg -framerate 10 -pattern_type glob -i '*.jpg' \
-c:v libx264 -vf "pad=ceil(iw/2)*2:ceil(ih/2)*2" -pix_fmt yuv420p output.mp4

Take snapshot from video

ffmpeg -i input.mp4 -y -f image2 -ss 00:00:08.010 -t 0.001 -s 352x240 snapshot.jpg

Frame and Speed

Specify start and end frames

ffmpeg -r 60 -f image2 -s 1920x1080 -start_number 1 -i pic%04d.png -vframes 1000 -vcodec libx264 -crf 25 -pix_fmt yuv420p output.mp4

Speed up 2x

ffmpeg -i input.mp4 -filter:v "setpts=0.5*PTS" -filter:a "atempo=2" outputX2.mp4

Speed up 4x

ffmpeg -i input.mp4 -filter:v "setpts=0.25*PTS" -filter:a "atempo=2,atempo=2" outputX4.mp4

Audio

WAV to MP3

ffmpeg -i input.wav -vn -ar 44100 -ac 2 -b:a 192k output.mp3

Add background music

ffmpeg -i audio.mp3 -i input.mp4 -filter_complex "[0:a][1:a]amerge,pan=stereo|c0<c0+c2|c1<c1+c3[out]" -map 1:v -map "[out]" -c:v copy -shortest output.mp4

Loop audio to match video length

ffmpeg -i video1.mp4 -stream_loop -1 -i audio2.mp3 -c:v copy -shortest -map 0:v -map 1:a output.mp4

Add looped background music to image

ffmpeg -loop 1 -i image.jpg -i background-music.mp3 -c:v libx264 -tune stillimage -c:a aac -b:a 192k -pix_fmt yuv420p -t 5 output.mp4

Text Overlays

DrawText Filter

-vf "drawtext=text='string1 string2 string3':expansion=normal:fontfile=foo.ttf:y=h-line_h-10:x=(mod(5*n\,w+tw)-tw):fontcolor=white:fontsize=40:shadowx=2:shadowy=2"

More examples:
Loop Text with DrawText

⸻

TODO Filters (placeholders)
	•	Grayscale
	•	Gray to RGB
	•	Rotate 90°
	•	Flip
	•	Flop
	•	Transparent background
	•	Resize

⸻

Split video into chunks

ffmpeg -i source-file.foo -ss 0 -t 600 first-10-min.m4v

Convert HLS to MP4

ffmpeg -i http://.../playlist.m3u8 -c copy -bsf:a aac_adtstoasc output.mp4



⸻

Tools

Coming soon.

⸻

Contributing

To contribute:
	1.	Open README.md: Edit Link
	2.	Click the edit button 

	3.	Make changes and commit 


⸻

References
	•	https://github.com/yangboz/imagemagick-cheatsheet
	•	https://ffmpeg.org/ffmpeg.html
	•	https://en.wikibooks.org/wiki/FFMPEG_An_Intermediate_Guide/image_sequence
	•	https://github.com/gradywoodruff/cheatsheet/blob/master/ffmpeg.md
	•	https://stackoverflow.com/questions/18123376/webm-to-mp4-conversion-using-ffmpeg

⸻

Known Issues
	•	libx264 height not divisible by 2

⸻
