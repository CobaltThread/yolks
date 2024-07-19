FROM        --platform=$TARGETOS/$TARGETARCH php:8.3.9-fpm-alpine3.20

LABEL       author="Alexander Featherston" maintainer="afeatherston@proton.me"
LABEL       org.opencontainers.image.source="https://github.com/cobaltthread/yolks"
LABEL       org.opencontainers.image.licenses=MIT

ADD --chmod=0755 https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/
RUN install-php-extensions gd xdebug xsl zip intl bz2 calendar mysqli pdo_mysql apcu redis imagick/imagick@master imap soap gmp bcmath exif mailparse

# Install base supplimentary packages
RUN         apk update \
            && apk upgrade \
            && apk add --no-cache \
            composer \
            mariadb \
            runuser \
            && adduser -D -h /home/container container

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./../entrypoint.sh /entrypoint.sh
CMD         [ "/bin/ash", "/entrypoint.sh" ]