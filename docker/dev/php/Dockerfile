FROM php:8.3.13-fpm-alpine

RUN apk update
RUN apk upgrade
RUN apk add bash git vim tzdata

# install extensions
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN install-php-extensions xdebug

RUN install-php-extensions opcache

# copy config
COPY ./docker/dev/php/php.ini $PHP_INI_DIR/php.ini

# install composer
RUN install-php-extensions @composer

# working directory
WORKDIR /var/www/html

# envs
ARG TZ

ENV TZ=${TZ}

# timezone and localtime
RUN echo $TZ > /etc/timezone
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime
