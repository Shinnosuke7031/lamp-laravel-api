FROM php:7.4-apache
ARG composer_ver=1.10.20
ARG composer_hash=e70b1024c194e07db02275dd26ed511ce620ede45c1e237b3ef51d5f8171348d
ARG composer_path=/usr/local/bin/composer

RUN apt-get update \
  && php -r "copy('https://getcomposer.org/download/$composer_ver/composer.phar', '$composer_path');" \
  && chmod 755 $composer_path \
  && php -r "if (hash_file('sha256', '$composer_path') !== '$composer_hash') { \
          echo '!!! Failed to install Composer !!!'; \
          unlink('$composer_path'); \
      } \
      echo PHP_EOL;" \
  && apt-get install -y vim \
  && apt-get install -y unzip \
  && docker-php-ext-install pdo_mysql \
  && a2enmod rewrite

COPY php.ini /usr/local/etc/php/
COPY /apache/httpd.conf /etc/apache2/sites-available/000-default.conf