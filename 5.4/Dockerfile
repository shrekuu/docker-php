FROM php:5.4-fpm

RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak \
    echo " " > /etc/apt/sources.list \
    echo "deb http://mirrors.aliyun.com/debian jessie main" >> /etc/apt/sources.list \
    echo "deb http://mirrors.aliyun.com/debian jessie-updates main" >> /etc/apt/sources.list

# Install PHP extensions and PECL modules.
RUN buildDeps=" \
        libbz2-dev \
        libmemcached-dev \
        libmysqlclient-dev \
        libsasl2-dev \
    " \
    runtimeDeps=" \
        curl \
        git \
        zip unzip \
        vim \
        libfreetype6-dev \
        libicu-dev \
        libjpeg-dev \
        libldap2-dev \
        libmcrypt-dev \
        libmemcachedutil2 \
        libpng12-dev \
        libpq-dev \
        libxml2-dev \
        libxslt1-dev \
    " \
    && apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y $buildDeps $runtimeDeps \
    && docker-php-ext-install bcmath bz2 calendar iconv intl mbstring mcrypt mysql mysqli pdo_mysql pdo_pgsql pgsql soap xsl zip sockets \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-install ldap \
    && docker-php-ext-install exif \
    && pecl install memcached-2.2.0 redis-4.3.0 zendopcache \
    && docker-php-ext-enable memcached.so redis.so opcache.so \
    && apt-get purge -y --auto-remove $buildDeps \
    && rm -r /var/lib/apt/lists/*

# install vimrc
RUN git clone https://gitee.com/shrekuu/amix-vimrc.git ~/.vim_runtime
RUN sh ~/.vim_runtime/install_awesome_vimrc.sh

# Install Composer.
ENV COMPOSER_ALLOW_SUPERUSER=1
  
RUN cd /opt \
  curl https://mirrors.cloud.tencent.com/composer/composer.phar -o /usr/local/bin/composer \
  chmod uga+x /usr/local/bin/composer
