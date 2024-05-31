# Record

## Screen Capture
```bash
# This is misleading as a shell script, at least for now
# Cause it's specifically for windows; and won't work on other platforms

# Suboptimal screengram method:
.\ffmpeg.exe -f gdigrab -i desktop -c:v h264_nvenc output.mkv
# To capture specific window by title (insted of whole desktop
.\ffmpeg.exe -f gdigrab -i title="Desktop" -c:v h264_nvenc output.mkv

# Using ddagrab, with FFMPEG 6.0 or later
.\ffmpeg.exe -filter_complex ddagrab=0 -c:v h264_nvenc output.mkv
# To record a specific part of the screen
.\ffmpeg.exe -filter_complex ddagrab=video_size=1280x720:offset_x=64:offset_y=64 -c:v h264_nvenc output.mkv
# To use ddagrab without hardware encoding
.\ffmpeg.exe -filter_complex ddagrab=0,hwdownload,format=bgra -c:v libx264 output.mkv
# ddagrab doesn't capture mouse cursor & exits immediately on mouse move; might be a bug

# For other platforms, see https://trac.ffmpeg.org/wiki/Capture/Desktop
```

## Convert Bitrate
```bash
# RECODE AT SPECIFIC BITRATE
ffmpeg -i input.mp4 -b:v 4M -c:a copy output.mp4
```


# Process

## Crop
```bash
# Generic syntax
ffmpeg -i in.mp4 -filter:v "crop=outW:outH:cropX:cropY" -c:a copy out.mp4
# Center-crop an HD video from UHD video
ffmpeg -i in.mp4 -filter:v "crop=1920:1080:960:540" -c:a copy out.mp4
```

## Retime
```bash
# The `setpts` video filter allows manipulating presentation timestamps
# It accepts various expressions; https://ffmpeg.org/ffmpeg-filters.html#setpts_002c-asetpts
# To retime clip to 60X here we are using PTS/60 to change the scale factor of the timestamp
# NOTE: -an is set to ignore audio, as is the case with most of the time I use this script
ffmpeg -i input.mp4 -vf "setpts=PTS/60" -an output.mp4
```

## Trim
```bash
# Seek to position: -ss HH:MM:SS
# Media time duration: -t HH:MM:SS
# Keep original encoding: -c copy (optional)
ffmpeg -ss 00:00:00 -t 00:00:10 -i input.mp4 -c copy output.mp4
# NOTE: it matters whether -ss is placed before or after the input
```

## Timelapse
```bash
# Frame Rate [required]
#   -framerate <fps_integer>
#
# Pattern Type [required]
#   -pattern_type glob
#   -pattern_type sequence -start_number <start_integer>
#
# Video Codec [recommended]
#   -c:v libx264 -crf 17
#   -c:v prores -profile:v 3
#   ...etc (use whatever is preferred... h.265 or even AV1 is fine as distribution format)
#
# Pixel Format [recommended]
#    -pix_fmt yuv422p10 (for mastering)
#    -pix_fmt yuv420p (for distribution)
#
# Color Space [optional]
#   -vf colorspace=all=bt709:iall=bt601-6-625:fast=1 -colorspace 1 -color_primaries 1 -color_trc 1
#
# Now, bring it all together...
ffmpeg -framerate 60 -pattern_type glob -i "./G00*.JPG" -c:v libx264 -crf 17 -pix_fmt yuv420p timelapse.mp4
```
