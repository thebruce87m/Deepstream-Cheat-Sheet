# Deepstream-Cheat-Sheet

# Docker

## Docker on x86 PC:

```bash

# Allow connections to X
xhost +

# Run the Deepstream Docker
docker run \
--gpus all \
-it \
--rm \
--privileged \
--net=host \
-v /tmp/.X11-unix:/tmp/.X11-unix \
-v $(pwd):/code/ \
-e DISPLAY=$DISPLAY \
-w /code \
nvcr.io/nvidia/deepstream:6.0-devel

# Gstreamer Dependencies
apt update && apt install -y \
build-essential \
cmake \
libprotobuf-dev \
protobuf-compiler \
libgstreamer-plugins-base1.0-dev \
libgstreamer1.0-dev \
libgstrtspserver-1.0-dev \
libx11-dev \
libjson-glib-dev
```

# RTSP Streams

## RTSP H265 with ximagesink

```bash
# Run the pipeline
gst-launch-1.0 -v \
\
\
rtspsrc location=rtsp://admin:password@192.168.250.100/Streaming/Channels/102 \
! rtph265depay \
! h265parse \
! nvv4l2decoder \
! nvvideoconvert \
! ximagesink
```
