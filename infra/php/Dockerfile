FROM php:7.4-fpm-buster
# コンテナイメージをビルドする際のイメージを指定
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]
# 実行 オプションを指定
ENV COMPOSER_ALLOW_SUPERUSER=1 \
    COMPOSER_HOME=/composer
# ENV命令はコンテナ内のサーバー環境変数を設定

COPY --from=composer:1.10 /usr/bin/composer /usr/bin/composer

RUN apt-get update && \
    apt-get -y install git unzip libzip-dev libicu-dev libonig-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/list/* && \
    docker-php-ext-install intl pdo_mysql zip bcmath
# Dockerfile内では apt は警告が表示されるので apt-get を使用


COPY ./php.ini /usr/local/etc/php/php.ini

WORKDIR /work
