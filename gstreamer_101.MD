
From camera to mp4 file gstream:
gst-launch-1.0 -v v4l2src device=/dev/video0 ! image/jpeg, width=1280, height=720 ! jpegdec ! x264enc ! mp4mux ! filesink location=video.mp4 -e



Split pipes:
gst-launch-1.0 -v v4l2src device=/dev/video0 ! image/jpeg, width=1280, height=720 ! jpegdec ! tee name=t t. ! queue ! x264enc ! mp4mux ! filesink location=video.mp4 t. ! queue  ! x264enc ! mp4mux ! filesink location=video1.mp4 -e


note: zero letancy needed on tee for x264 encode for everything to work
gst-launch-1.0 v4l2src -v device=/dev/video0 ! image/jpeg, width=1280, height=720 ! jpegdec ! tee name=t t. ! queue ! x264enc tune=zerolatency ! mp4mux ! filesink location=video.mp4 t. ! queue ! xvimagesink -e
