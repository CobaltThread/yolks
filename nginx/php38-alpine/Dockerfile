FROM        --platform=$TARGETOS/$TARGETARCH php:8.3.9-fpm-alpine3.20

LABEL       author="Alexander Featherston" maintainer="afeatherston@proton.me"
LABEL       org.opencontainers.image.source="https://github.com/cobaltthread/yolks"
LABEL       org.opencontainers.image.licenses=MIT

# Install base supplimentary packages
RUN         apk update \
            && apk upgrade \
            && apk add --no-cache \
            curl \
            ca-certificates \
            php83 \
            php83-bcmath \
            php83-bz2 \
            php83-calendar \
            php83-common \
            php83-ctype \
            php83-curl \
            php83-dom \
            php83-exif \
            php83-fileinfo \
            php83-gd \
            php83-gettext \
            php83-gmp \
            php83-iconv \
            php83-json \
            php83-mbstring \
            php83-mysqli \
            php83-mysqlnd \
            php83-odbc \
            php83-openssl \
            php83-pdo \
            php83-pdo_mysql \
            php83-pdo_dblib \
            php83-pdo_odbc \
            php83-pdo_pgsql \
            php83-pdo_sqlite \
            php83-phar \
            php83-session \
            php83-simplexml \
            php83-soap \
            php83-sqlite3 \
            php83-tokenizer \
            php83-xml \
            php83-zip \
            mariadb \
            && adduser -D -h /home/container container

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./../entrypoint.sh /entrypoint.sh
CMD         [ "/bin/ash", "/entrypoint.sh" ]