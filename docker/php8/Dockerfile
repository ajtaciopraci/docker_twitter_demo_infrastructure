FROM alpine:latest
RUN \
    apk add --no-cache \
    apache2-proxy \
    apache2-ssl \
    apache2-utils \
    curl \
    git \
    logrotate \
    php8 \
    php8-cli \
    openssl \
    openssh \
    bash  \
    openrc \
    mc 


RUN apk add --no-cache \
php8-mysqli php8-pdo_mysql \
php8-zip \
php8-bcmath \
php8-opcache \
php8-intl \
php8-gd \
php8-sodium \
php8-bcmath \
php8-zip \
php8-sockets \
php8-exif \
php8-imap \
php8-phar \
php8-pear \
php8-curl \
php8-iconv \
php8-redis \
php8-simplexml \
php8-ctype \
php8-dom \
php8-fileinfo \
php8-xmlreader \
php8-xmlwriter \
php8-tokenizer \
php8-sockets




#setup php as default cli
RUN ln -s /usr/bin/php8 /usr/bin/php

# Installing composer and prestissimo globally
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
ENV COMPOSER_ALLOW_SUPERUSER=1 COMPOSER_MEMORY_LIMIT=-1


RUN git clone https://github.com/ajtaciopraci/docker_twitter_demo.git /var/www/web



#apache2
RUN apk add php8-apache2

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/www/log
RUN mkdir  /var/www/log
RUN chmod 0777  /var/www/web/log
RUN chmod 0777  /var/www/web/temp
COPY conf.d/httpd.conf /etc/apache2/httpd.conf
COPY conf.d/php.ini /etc/php8/php.ini

COPY conf.d/local.neon /var/www/web/config
RUN cd /var/www/web && composer update

WORKDIR /var/www/web/www

EXPOSE 80

CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
