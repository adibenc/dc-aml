FROM php:8.2-fpm-bullseye
#FROM php:7.4-fpm

LABEL maintainer="M Adib<adib35785@gmail.com>"

RUN apt-get update
RUN apt-get install -y vim
RUN apt-get install -y libtidy-dev gpg libpng-dev libpq-dev vim git exiftool libzip-dev libaio1 ldap-utils libldap2-dev unzip
RUN apt-get install -y libjpeg-dev libwebp-dev libjpeg62-turbo-dev libxpm-dev libfreetype6-dev
RUN docker-php-ext-configure gd --with-jpeg
RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql 
RUN docker-php-ext-configure exif
RUN docker-php-ext-install tidy pdo pdo_pgsql pgsql sockets pdo_mysql mysqli exif gd zip ldap
# RUN docker-php-ext-install libjpeg62-turbo-dev
RUN docker-php-ext-enable exif
RUN apt-get update && apt-get install -y ntp

# internationalizesyen
RUN set -eux; \
    apt-get update; \
    apt-get install -y\
        libicu-dev; \
    docker-php-ext-install intl; \
    rm -rf /var/lib/apt/lists/*;

RUN echo "memory_limit=-1" > "$PHP_INI_DIR/conf.d/memory-limit.ini" \
&& echo "date.timezone=Asia/Jakarta" > "$PHP_INI_DIR/conf.d/date_timezone.ini" \
&& echo "short_open_tag=Off" > "$PHP_INI_DIR/conf.d/short_open_tag.ini"

ENV TZ=Asia/Jakarta
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN dpkg-reconfigure --frontend noninteractive tzdata
# RUN sed -i 's/pool 0.*/pool ntp.metrologi.lipi.go.id/g' /etc/ntp.conf 

COPY composer-setup.php .
#RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
#RUN php -v
#RUN php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
#RUN php -r "unlink('composer-setup.php');"

RUN php -m
RUN php -r "print_r(gd_info());"
