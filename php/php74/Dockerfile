FROM php:7.4-fpm

LABEL maintainer="Zhuo Zhang"

WORKDIR /var/www/http

ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

FROM php:7.4-fpm
RUN echo "deb http://mirrors.aliyun.com/debian/ buster main non-free contrib \n \
deb-src http://mirrors.aliyun.com/debian/ buster main non-free contrib \n \
deb http://mirrors.aliyun.com/debian-security buster/updates main \n \
deb-src http://mirrors.aliyun.com/debian-security buster/updates main \n \
deb http://mirrors.aliyun.com/debian/ buster-updates main non-free contrib \n \
deb-src http://mirrors.aliyun.com/debian/ buster-updates main non-free contrib \n \
deb http://mirrors.aliyun.com/debian/ buster-backports main non-free contrib \n \
deb-src http://mirrors.aliyun.com/debian/ buster-backports main non-free contrib" > /etc/apt/sources.list \
    # 更新及安装库
    && apt-get update \
    && apt-get install -y \
    vim net-tools \
    build-essential \
    libmagickcore-dev \
    libmagickwand-dev \
    imagemagick \
    libmcrypt-dev \
    libzip-dev \
    libmemcached-dev \
    supervisor  --fix-missing \
    # GD库扩展
    && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    && docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    # PHP扩展安装
    && docker-php-ext-install -j$(nproc) bcmath calendar exif gettext sockets dba mysqli pcntl pdo_mysql shmop sysvmsg sysvsem sysvshm iconv \
    && pecl install memcached-3.1.4 \
    && pecl install redis-5.2.2 \
    && pecl install imagick mcrypt zip swoole \
    && docker-php-ext-enable memcached redis imagick mcrypt zip swoole \
    && pecl install xdebug \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && composer global require laravel/installer \
    && apt-get clean \
    && apt-get autoclean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# 一些php脚本的配置
COPY conf/php.ini /etc/php/7.4/cli/conf.d/99-www-data.ini
COPY conf/xdebug.ini /usr/local/etc/php/conf.d/90-xdebug.ini
# supervisord配置
#COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
# 脚本
COPY sh/start-container /usr/local/bin/start-container
RUN chmod +x /usr/local/bin/start-container

EXPOSE 9000

ENTRYPOINT ["start-container"]
