FROM cdrage/ffmpeg

RUN apk add --no-cache --update ttf-droid

COPY ./docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["/bin/ash"]
