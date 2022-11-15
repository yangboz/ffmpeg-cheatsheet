# ffmpeg-cheatsheet

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
