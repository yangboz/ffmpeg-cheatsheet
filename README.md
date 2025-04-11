# FFMPEG Cheatsheet

> For single image processing, check: [ImageMagick Cheatsheet]()

## Table of Contents
- [Why FFMPEG?](#why-ffmpeg)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Best Practices](#best-practices)
- [Tools](#tools)
- [Contributing](#contributing)
- [References](#references)
- [Known Issues](#known-issues)

## Why FFMPEG?

FFmpeg is the leading multimedia framework, able to:
- Decode, encode, transcode
- Mux, demux, stream
- Filter and play almost any media format

**Key Features:**
- Highly portable (Linux, macOS, Windows, BSDs, Solaris)
- Complete cross-platform solution
- Supports ancient to cutting-edge formats

> **TL;DR**: Converting video and audio has never been so easy.

## Installation

### Linux
```bash
# Debian/Ubuntu
apt-get install ffmpeg

# CentOS/RHEL
yum install ffmpeg
```

### macOS
```bash
brew install ffmpeg
```

### Windows
Download from [FFmpeg Windows Builds]()

## Cheatsheet

### Basic Syntax
```bash
ffmpeg [global_options] {[input_file_options] -i input_url} ... {[output_file_options] output_url}
```

### Common Operations

#### Get File Info
```bash
ffmpeg -i input.mp4
```

#### Format Conversion
```bash
# MP4 to AVI
ffmpeg -i input.mp4 output.avi

# GIF to MP4
ffmpeg -i animated.gif -movflags faststart -pix_fmt yuv420p -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" video.mp4

# WEBM to MP4
ffmpeg -i movie.webm movie.mp4
```

### Image Operations

#### Extract Frames
```bash
# Extract all frames
ffmpeg -i video.mpg image-%04d.jpg

# Take single snapshot
ffmpeg -i input.mp4 -y -f image2 -ss 00:00:08.010 -t 0.001 -s 352x240 snapshot.jpg
```

#### Create Video from Images
```bash
# From PNGs
ffmpeg -framerate 30 -pattern_type glob -i '*.png' -c:v libx264 -pix_fmt yuv420p out.mp4

# From JPGs with padding
ffmpeg -framerate 10 -pattern_type glob -i '*.jpg' \
    -c:v libx264 -vf "pad=ceil(iw/2)*2:ceil(ih/2)*2" -pix_fmt yuv420p output.mp4
```

### Audio Operations

```bash
# WAV to MP3
ffmpeg -i input.wav -vn -ar 44100 -ac 2 -b:a 192k output.mp3

# Add background music
ffmpeg -i audio.mp3 -i input.mp4 -filter_complex "[0:a][1:a]amerge,pan=stereo|c0<c0+c2|c1<c1+c3[out]" \
    -map 1:v -map "[out]" -c:v copy -shortest output.mp4
```

## Known Issues
- libx264 height not divisible by 2
- [Add more issues here]

## References
- [FFmpeg Official Documentation](https://ffmpeg.org/ffmpeg.html)
- [FFmpeg Intermediate Guide](https://en.wikibooks.org/wiki/FFMPEG_An_Intermediate_Guide/image_sequence)
- [ImageMagick Cheatsheet](https://github.com/yangboz/imagemagick-cheatsheet)
