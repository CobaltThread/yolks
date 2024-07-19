FROM        --platform=$TARGETOS/$TARGETARCH php:8.3.9-fpm-alpine3.20

LABEL       author="Alexander Featherston" maintainer="afeatherston@proton.me"
LABEL       org.opencontainers.image.source="https://github.com/cobaltthread/yolks"
LABEL       org.opencontainers.image.licenses=MIT

ADD --chmod=0755 https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/
RUN install-php-extensions gd xdebug dom iconv xsl mbstring ctype zip pdo xml curl intl bz2 calendar exif fileinfo json mysqli mysql posix tokenizer xmlwriter xmlreader phar soap mysql gmp bcmath apcu redis imagick imap

# Install base supplimentary packages
RUN         apk update \
            && apk upgrade \
            && apk add --no-cache \
            composer \
            && adduser -D -h /home/container container

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./../entrypoint.sh /entrypoint.sh
CMD         [ "/bin/ash", "/entrypoint.sh" ]