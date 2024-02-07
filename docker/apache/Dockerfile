FROM php:8.1-apache-bullseye

COPY --from=composer:2.6 /usr/bin/composer /usr/bin/composer

RUN apt-get update \
  && apt-get install -y zlib1g-dev libzip-dev unzip sudo\
  && docker-php-ext-install zip

# a2emod rewrite をして apache に rewrite モジュールを追加
# これをしないと Laravel でルート以外にアクセスできない
RUN a2enmod rewrite

# docker php には mysql 用のドライバが未インストールのため追加する
RUN docker-php-ext-install pdo_mysql

ADD docker/apache/php.ini /usr/local/etc/php/

# Apache の conf は seites-available に作成し
# a2ensite コマンドでシンボリックリンクを sites-enabled に作成する
ADD docker/apache/config/000-default.conf /etc/apache2/sites-available/
RUN a2ensite 000-default

COPY ./src/dondake /var/www/html

WORKDIR /var/www/html

# Make port 80 available to the world outside this container
EXPOSE 80

ENV COMPOSER_ALLOW_SUPERUSER 1

RUN chown www-data storage/ -R \
  && composer install --no-scripts --no-interaction