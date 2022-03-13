FROM php:7.3-fpm

RUN pecl install xdebug
COPY xdebug.ini /usr/local/etc/php/conf.d/90-xdebug.ini

# 安装基础环境,设置时区
RUN apt-get update && apt-get install zlib1g-dev -y \
        libmcrypt-dev \
        libmemcached-dev \
        libpq-dev \
        libwebp-dev \
        libjpeg-dev \
        libpng-dev \
        libfreetype6-dev \
        libzip-dev \
        libxml2-dev \
        git \
        libicu-dev \
        xvfb libfontconfig \
        libgmp-dev \
        vim \
        procps \
        nginx \
        cron \
        sudo \
        supervisor && \
     docker-php-ext-install  pdo && \
     docker-php-ext-install  pdo_mysql &&  \
     docker-php-ext-configure gd --with-webp-dir=/usr/include/webp --with-jpeg-dir=/usr/include --with-png-dir=/usr/include --with-freetype-dir=/usr/include/freetype2 && \
     docker-php-ext-install  gd && \
     docker-php-ext-install  exif && \
     docker-php-ext-install  zip && \
     docker-php-ext-install  gmp && \
     docker-php-ext-install  bcmath && \
     docker-php-ext-install  pcntl && \
     docker-php-ext-install  soap && \
     docker-php-ext-install  sockets && \
     docker-php-ext-configure intl && \
     docker-php-ext-install intl && \
#     pecl install mongodb && \
#     echo "extension=mongodb.so" > /usr/local/etc/php/conf.d/docker-php-ext-mongodb.ini && \
     pecl install -o -f igbinary && \
     docker-php-ext-enable igbinary && \
#     docker-php-ext-enable opcache && \
     pecl install --onlyreqdeps --nobuild redis-5.2.1 && \
     cd "$(pecl config-get temp_dir)/redis" && phpize && \
     ./configure --enable-redis-igbinary && make && make install && \
     docker-php-ext-enable redis && \
#     pecl install --onlyreqdeps --nobuild memcached && \
#     cd "$(pecl config-get temp_dir)/memcached" && phpize && \
#     ./configure --enable-memcached-igbinary --enable-memcached-json --with-libdir=lib64 && make && make install && \
#     docker-php-ext-enable memcached && \
#     rm -rf /tmp/pear &&  \
     apt-get clean && \
     apt-get autoclean && \
     rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
     curl -sS https://getcomposer.org/installer | \
     php -- --install-dir=/usr/bin/ --filename=composer --version=1.10.13
#     crontab -l | { cat; echo "* * * * * sudo -u www-data /usr/local/bin/php /var/www/html/artisan schedule:run >> /dev/null 2>&1"; } | crontab - && \
#     sed -i '/session    required     pam_loginuid.so/c\#session    required     pam_loginuid.so/' /etc/pam.d/cron
#     ln -sf /usr/share/zoneinfo/America/Los_Angeles /etc/localtime && \
#     echo "America/Los_Angeles" > /etc/timezone

#COPY deploy/binaries/amazon-elasticache-cluster-client.so /usr/local/lib/php/extensions/no-debug-non-zts-20170718/
# git权限校验文件
COPY ./composer/auth.json /root/.composer/auth.json

WORKDIR /var/www/http
# COPY .ssh /root/.ssh/
#COPY deploy/composer.deploy.json ./composer.json
#RUN php -d memory_limit=-1 /usr/bin/composer install --no-dev

# 覆盖原有配置
#COPY deploy/nginxconfig/default.conf /etc/nginx/sites-enabled/default
#COPY deploy/phpconfig/php.ini /usr/local/etc/php/php.ini
#COPY deploy/phpconfig/php.conf /usr/local/etc/php-fpm.d/www.conf
#COPY deploy/supervisor/queue.conf /etc/supervisor/conf.d/queue.conf

#COPY --chown=www-data:www-data . .
#RUN mv .env.$stage_name .env && \
#     rm -f  /root/.ssh/* && \
#     rm -rf .ssh && \
#    sed -i "s/ENV_ID/$env_id/g" /var/www/html/.env && \
#    chmod 0777 /var/www/html/storage &&  \
#    chmod 0777 /var/www/html/public &&  \
#    composer dump-autoload && \
#    php artisan menu:auto && \
#    php artisan migrate
#    /usr/local/bin/php /var/www/html/artisan config:cache && \
#    /usr/local/bin/php /var/www/html/artisan route:cache

#ENTRYPOINT ["./deploy/entrypoint.sh"]
CMD ["php-fpm"]
