FROM        --platform=$TARGETOS/$TARGETARCH composer:lts

LABEL       author="Alexander Featherston" maintainer="afeatherston@proton.me"
LABEL       org.opencontainers.image.source="https://github.com/cobaltthread/yolks"
LABEL       org.opencontainers.image.licenses=MIT

#ENV GOSU_VERSION 1.11

#RUN adduser uvdesk -q --disabled-password --gecos ""

# Install base supplimentary packages
RUN         apk update \
            && apk upgrade \
            && adduser -D -h /home/container container

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./../entrypoint.sh /entrypoint.sh
CMD         [ "/bin/ash", "/entrypoint.sh" ]