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
            if [ -f /home/container/.my.cnf ]; then \
                echo -e "moving current config for install" \
                mv /home/container/.my.cnf /home/container/custom.my.cnf \
                runuser -l container -c 'curl https://raw.githubusercontent.com/parkervcp/eggs/master/database/sql/mariadb/install.my.cnf > /home/container/.my.cnf' \
                else \
                runuser -l container -c 'curl https://raw.githubusercontent.com/parkervcp/eggs/master/database/sql/mariadb/install.my.cnf > /home/container/.my.cnf' \
            fi \
            \
            echo -e "installing mysql database" \
            runuser -l container -c 'mkdir -p /home/container/run/mysqld' \
            runuser -l container -c 'mkdir -p /home/container/log/mysql' \
            runuser -l container -c 'mkdir /home/container/mysql' \
            \
            runuser -l container -c 'mysql_install_db --defaults-file=/home/container/.my.cnf' \
            \
            if [ -f /mnt/server/custom.my.cnf ]; then \
                echo -e "moving current config back in place" \
                mv /home/container/custom.my.cnf /home/container/.my.cnf \
            else \
                curl https://raw.githubusercontent.com/parkervcp/eggs/master/database/sql/mariadb/my.cnf > /home/container/.my.cnf \
            fi \
            \
            echo -e "install complete"

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./../entrypoint.sh /entrypoint.sh
CMD         [ "/bin/ash", "/entrypoint.sh" ]