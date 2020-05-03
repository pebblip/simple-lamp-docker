FROM php:7.3-apache

COPY --from=composer /usr/bin/composer /usr/bin/composer

ENV PROJECT_ROOT /opt/myproject
ENV APACHE_DOCUMENT_ROOT ${PROJECT_ROOT}/public

RUN mkdir -p ${APACHE_DOCUMENT_ROOT}

WORKDIR ${PROJECT_ROOT}

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

RUN apt update && apt-get install -y nodejs npm && \
docker-php-ext-install pdo_mysql && docker-php-ext-install mbstring

RUN a2enmod rewrite
