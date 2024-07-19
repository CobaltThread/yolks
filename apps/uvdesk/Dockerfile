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

RUN         echo -e "getting my.conf" \
            runuser -l container -c 'mkdir -p /mnt/temphome' \
            runuser -l container -c 'curl https://raw.githubusercontent.com/parkervcp/eggs/master/database/sql/mariadb/install.my.cnf > /mnt/temphome/.my.cnf' \
            echo -e "installing mysql database" \
            runuser -l container -c 'mkdir -p /mnt/temphome/run/mysqld' \
            runuser -l container -c 'mkdir -p /mnt/temphome/log/mysql' \
            runuser -l container -c 'mkdir /mnt/temphome/mysql' \
            runuser -l container -c 'mysql_install_db --defaults-file=/mnt/temphome/.my.cnf' \
            curl https://raw.githubusercontent.com/parkervcp/eggs/master/database/sql/mariadb/my.cnf > /mnt/temphome/.my.cnf \
            echo -e "install complete"

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./../entrypoint.sh /entrypoint.sh
CMD         [ "/bin/ash", "/entrypoint.sh" ]