FROM php:7.0-fpm

RUN apt-get update && \
    apt-get install -y libicu-dev libpq-dev zlib1g-dev && \
    docker-php-ext-install bcmath intl pdo_pgsql zip calendar

RUN apt-get update && apt-get install -y git unzip
ADD https://getcomposer.org/download/1.3.2/composer.phar /usr/local/bin/composer
RUN echo "6a4f761aa34bb69fca86bc411a5e9836ca8246f0fcd29f3804b174fee9fb0569 /usr/local/bin/composer" | sha256sum -c - && chmod 755 /usr/local/bin/composer

RUN apt-get update && \
    apt-get install -y libxrender1 libfontconfig libXext6 xz-utils && \
    curl -f "http://download.gna.org/wkhtmltopdf/0.12/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz" | tar -x -J --strip-components=1 -C /usr/local wkhtmltox/bin

RUN yes | pecl install xdebug
COPY docker-entrypoint.sh /usr/local/bin/
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["php-fpm"]