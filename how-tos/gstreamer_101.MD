## Gstreamer 1.0 commands:
* Pipeline-based multimedia framework that links together a wide variety of media processing systems to complete complex workflows.


### Pipe for camera to mp4 file:
``` bash
gst-launch-1.0 -v v4l2src device=<device> ! image/jpeg, width=1280, height=720 ! jpegdec ! x264enc ! mp4mux ! filesink location=<file_name> -e
# <device>: path where device is mounted (eg. /dev/video0)
# <file_name>: name of file where stream will be written (eg. video.mp4)
# -v: verbose mode, extra information
# -e: when present sends eos on ctrl + c, that is needed in order for headers to be written to file

# Pipe parts:
# v4l2src: used for reading from camera
# image/jpeg, width=1280, height=720: from meny configurations from v4l2src use this configuration
# jpegdec: decode raw stream from camera to jpeg (with this approach we can use this pipe on majority of cameras)
# x264enc: encoder for x264
# mp4mux: this element merges stream in mp4 format
# filesink: writes to file
```


### Split pipe for showing camera stream and recording it to mp4 file:
``` bash
gst-launch-1.0 v4l2src -v device=<device> ! image/jpeg, width=1280, height=720 ! jpegdec ! tee name=t t. ! queue ! x264enc tune=zerolatency ! mp4mux ! filesink location=<file_name> t. ! queue ! xvimagesink -e
# <device>: path where device is mounted (eg. /dev/video0)
# <file_name>: name of file where stream will be written (eg. video.mp4)
# -v: verbose mode, extra information
# -e: when present sends eos on ctrl + c, that is needed in order for headers to be written to file

# Pipe parts:
# v4l2src: used for reading from camera
# image/jpeg, width=1280, height=720: from meny configurations from v4l2src use this configuration
# jpegdec: decode raw stream from camera to jpeg (with this approach we can use this pipe on majority of cameras)
# tee: split pipe into two (every pipe starts with name (t))
# queue: queuing of data (new thread will be created so producer/consumer work in parallel)
# x264enc: encoder for x264 (note: zero letancy needed on tee for x264 encode for everything to work)
# mp4mux: this element merges stream in mp4 format
# filesink: writes to file
# xvimagesink: element used fou ui representation of camera stream
```
