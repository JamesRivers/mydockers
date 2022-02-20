# Destreamer 
Needed to download a number of MS Streams.  
Dockerfile listed - note I am not keeping this up to date use at own risk. 
Dockerhub link 

## Use 
```bash
ocker run -ti --rm -e DISPLAY=unix$DISPLAY --volume /tmp/.X11-unix:/tmp/.X11-unix --volume $(pwd):/download testdestreamer /destreamer/destreamer.sh -i "https://web.microsoftstream.com/video/VIDEO-ID" -o /download -u user@mail.com
```