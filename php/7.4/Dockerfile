FROM        --platform=$TARGETOS/$TARGETARCH php:8.4-rc-alpine3.20

LABEL       author="Alexander Featherston" maintainer="afeatherston@proton.me"

LABEL       org.opencontainers.image.source="https://github.com/cobaltthread/yolks"
LABEL       org.opencontainers.image.licenses=MIT

RUN         apk add --update --no-cache ca-certificates curl git openssl sqlite tar tzdata iproute2 \
				&& adduser -D -h /home/container container

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

STOPSIGNAL SIGINT

COPY        ./../entrypoint.sh /entrypoint.sh
CMD         [ "/bin/ash", "/entrypoint.sh" ]
