# ffmpeg-cheatsheet

for single image, please check:https://github.com/yangboz/imagemagick-cheatsheet

FFMPEG Cheatsheet.

**Want to improve this cheat sheet?  See the [Contributing](#contributing) section!**

## Table of Contents

* [Why FFMPEG?](#why-ffmpeg)
* [Prerequisites](#prerequisites)
* [Installation](#installation)
* [Best Practices](#cheatsheet)
* [Tools](#tools)
* [Contributing](#contributing)

## Why FFMPEG

FFmpeg is the leading multimedia framework, able to decode, encode, transcode, mux, demux, stream, filter and play pretty much anything that humans and machines have created. It supports the most obscure ancient formats up to the cutting edge. No matter if they were designed by some standards committee, the community or a corporation. It is also highly portable: FFmpeg compiles, runs, and passes our testing infrastructure FATE across Linux, Mac OS X, Microsoft Windows, the BSDs, Solaris, etc. under a wide variety of build environments, machine architectures, and configurations.

A complete, cross-platform solution to record, convert and stream audio and video.
Converting video and audio has never been so easy.

TL;NR

## Prerequisites

https://ffmpeg.org/documentation.html

### Video format

mp4,avi,mpeg,flv...

### Video Processing

### Video codec

TL;NR

## Installation

http://ffmpeg.org/download.html

### Linux

```
apt-get install ffmpeg
```

```
yum install ffmpeg
```

### MacOS

 ```
 brew install ffmpeg
 ```

### Windows

https://ffmpeg.org/download.html#build-windows

#### Memory Constraints


#### Overview

```
 _______              ______________
|       |            |              |
| input |  demuxer   | encoded data |   decoder
| file  | ---------> | packets      | -----+
|_______|            |______________|      |
                                           v
                                       _________
                                      |         |
                                      | decoded |
                                      | frames  |
                                      |_________|
 ________             ______________       |
|        |           |              |      |
| output | <-------- | encoded data | <----+
| file   |   muxer   | packets      |   encoder
|________|           |______________|

```

### Cheatsheet

ffmpeg [global_options] {[input_file_options] -i input_url} ... {[output_file_options] output_url} ...

### Info

```ffmpeg info```

####  mp4 to avi:

```
ffmpeg -i input.mp4 output.avi
```

####  gif to mp4:

```
ffmpeg -i animated.gif -movflags faststart -pix_fmt yuv420p -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" video.mp4
```

####  webm to mp4:

```
ffmpeg -i movie.webm movie.mp4
```

#### Resize:

```
```

#### Extract to images

```
ffmpeg -i video.mpg image-%04d.jpg 
```
#### pngs to video
```
ffmpeg -framerate 30 -pattern_type glob -i '*.png' \
  -c:v libx264 -pix_fmt yuv420p out.mp4
```

#### take snapshot of video

```
ffmpeg -i VID_20200720_092249.mp4 -y -f image2 -ss 08.010 -t 0.001 -s 352x240 b.jpg
```


#### Specifying start and end frames
```
ffmpeg -r 60 -f image2 -s 1920x1080 -start_number 1 -i pic%04d.png -vframes 1000 -vcodec libx264 -crf 25  -pix_fmt yuv420p output.mp4
```


### jpgs to video with video filter

```
ffmpeg -framerate 10 -pattern_type glob -i '*.jpg' \
  -c:v libx264 -vf "pad=ceil(iw/2)*2:ceil(ih/2)*2"  -pix_fmt yuv420p out609cfbgs.mp4

``` 


### jpgs to video with video filter

```
ffmpeg -framerate 10 -pattern_type glob -i '*.jpg' \
  -c:v libx264 -vf "pad=ceil(iw/2)*2:ceil(ih/2)*2"  -pix_fmt yuv420p out609cfbgs.mp4

``` 

### add background music 

```
ffmpeg -i audio.mp3 -i input.mp4 -filter_complex "[0:a][1:a]amerge,pan=stereo|c0<c0+c2|c1<c1+c3[out]" -map 1:v -map "[out]" -c:v copy -shortest output.mp4

``` 
#### LOOP AUDIO TO THE LENGTH OF VIDEO

```
ffmpeg \
    -i video1.mp4 -stream_loop -1 -i audio2.mp3 \
    -c:v copy \
    -shortest \
    -map 0:v -map 1:a \
    -y output.mp4
```


### add loop background music to image


```
ffmpeg -loop 1 -i image.jpg -i background-music.mp3 \-c:v libx264 -tune stillimage -c:a aac -b:a 192k -pix_fmt yuv420p \-t 5 out-image.mp4

``` 

``` 

#### drawtext filter

```
 -vf "drawtext=text=string1 string2 string3 string4 string5 string6 string7 :expansion=normal:fontfile=foo.ttf: y=h-line_h-10:x=(mod(5*n\,w+tw)-tw): fontcolor=white: fontsize=40: shadowx=2: shadowy=2"
```

@more: https://superuser.com/questions/875058/loop-text-that-wipes-left-to-right-using-ffmpeg-drawtext-filter/1026470#1026470

#### GrayScale


#### Gray to RGB

#### Rotate 90

#### Flip


#### Flop

#### Resize

#### fasten video and audio

2X
```
ffmpeg -i input.mp4   -filter:v "setpts=0.5*PTS" -filter:a "atempo=2" outputX2.mp4 
```

4X
```
ffmpeg -i input.mp4   -filter:v "setpts=0.25*PTS" -filter:a "atempo=2, atempo=2" outputX4.mp4 
```

#### split video into X minutes chunks

```
 ffmpeg -i source-file.foo -ss 0 -t 600 first-10-min.m4v
```

#### Background Transparent



## Contributing

Here's how to contribute to this cheat sheet.

### Open README.md

Click [README.md](https://github.com/wsargent/docker-cheat-sheet/blob/master/README.md) <-- this link

![Click This](images/click.png)

### Edit Page

![Edit This](images/edit.png)

### Make Changes and Commit

![Change This](images/change.png)

![Commit](images/commit.png)

### Tools

## References

https://github.com/yangboz/imagemagick-cheatsheet

https://ffmpeg.org/ffmpeg.html

https://en.wikibooks.org/wiki/FFMPEG_An_Intermediate_Guide/image_sequence

https://github.com/gradywoodruff/cheatsheet/blob/master/ffmpeg.md

https://stackoverflow.com/questions/18123376/webm-to-mp4-conversion-using-ffmpeg

### known issues

https://stackoverflow.com/questions/20847674/ffmpeg-libx264-height-not-divisible-by-2
