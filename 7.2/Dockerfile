FROM php:7.2-fpm

RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak \
    touch /etc/apt/sources.list
RUN echo "deb http://mirrors.aliyun.com/debian jessie main" >> /etc/apt/sources.list
RUN echo "deb http://mirrors.aliyun.com/debian jessie-updates main" >> /etc/apt/sources.list

# Download script to install PHP extensions and dependencies
ADD https://raw.githubusercontent.com/mlocati/docker-php-extension-installer/master/install-php-extensions /usr/local/bin/

RUN chmod uga+x /usr/local/bin/install-php-extensions && sync

RUN DEBIAN_FRONTEND=noninteractive apt-get update -q \
    && DEBIAN_FRONTEND=noninteractive apt-get install -qq -y \
      curl \
      git \
      vim \
      zip unzip \
    && install-php-extensions \
      bcmath \
      bz2 \
      calendar \
      exif \
      gd \
      intl \
      ldap \
      memcached \
      mysqli \
      opcache \
      pdo_mysql \
      pdo_pgsql \
      pgsql \
      redis \
      soap \
      xsl \
      zip \
      sockets \
      pdo_sqlsrv \
      sqlsrv
# already installed:
#      iconv \
#      mbstring \

# install vimrc
RUN git clone https://gitee.com/shrekuu/amix-vimrc.git ~/.vim_runtime
RUN sh ~/.vim_runtime/install_awesome_vimrc.sh

# Install Composer.
ENV COMPOSER_ALLOW_SUPERUSER=1
  
RUN cd /opt \
  curl https://mirrors.cloud.tencent.com/composer/composer.phar -o /usr/local/bin/composer \
  chmod uga+x /usr/local/bin/composer
