FROM php:7.4-cli

WORKDIR /var/www/html/php/public

EXPOSE 80

COPY . /var/www/html/php
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf
COPY php.ini /usr/local/etc/php/php.ini

#RUN php -r "if (hash_file('sha384', 'composer-setup.php') ==='795f976fe0ebd8b75f26a6dd68f78fd3453ce79f32ecb33e7fd087d39bfeb978342fb73ac986cd4f54edd0dc902601dc') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        libzip-dev \
        default-mysql-client \
        less \
        wget \
        && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* 

RUN docker-php-ext-configure zip && \
    docker-php-ext-install zip && \
    docker-php-ext-install pdo_mysql && \
    pecl install xdebug && \
    docker-php-ext-enable xdebug

ENV DOCKERIZE_VERSION v0.6.1
ENV PHP_CLI_SERVER_WORKERS 30
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

RUN composer install
CMD ["composer","start"]