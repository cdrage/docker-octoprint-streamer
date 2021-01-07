FROM alpine:3.12.3 as builder

MAINTAINER Adi Linden <adi@adis.ca>

RUN apk add --no-cache curl ffmpeg py-pip

# Songs picked from YouTube Audio Library
# https://www.youtube.com/audiolibrary/music
WORKDIR /music/edm
RUN pip install youtube-dl
RUN youtube-dl --extract-audio --audio-format mp3 -o "/music/edm/%(id)s.%(ext)s" https://www.youtube.com/watch?v=mI8f9AB7_yU

WORKDIR /
RUN z=0; \
    for i in $(ls -1 /music/*/*.mp3); do \
        if [ $z -gt 0 ]; then \
            printf "|%s" "$i" >> /music/all.txt; \
        else \
            printf "%s" "$i" >> /music/all.txt; \
        fi; \
        z=1; \
    done
RUN LIST=$(head -1 /music/all.txt); ffmpeg -i "concat:$LIST" -acodec copy /music/all.mp3

###

FROM busybox

WORKDIR /music
COPY --from=builder /music/ /music

CMD ["/bin/ash"]
