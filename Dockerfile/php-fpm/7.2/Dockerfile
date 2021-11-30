# The Base Image
FROM php:7.2-fpm

# The Maintainer
LABEL maintainer="JohnHe China <564079964@qq.com>"

# Timezone
ARG TIMEZONE
ENV TIMEZONE=${TIMEZONE:-"Asia/Shanghai"}

# Install dependencies and tools
RUN sed -i "s@/deb.debian.org/@/mirrors.aliyun.com/@g" /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        libz-dev \
        libpq-dev \
        libpng-dev \
        libfreetype6-dev \
        libssl-dev \
        libgmp-dev \
        libbz2-dev \
        libcurl4-openssl-dev \
        libicu-dev \
        libjpeg62-turbo-dev \
        libldap2-dev \
        libmcrypt-dev \
        libmemcached-dev \
        libncurses5-dev \
        libxml2-dev \
        libxslt-dev \
        netcat \
        unzip \
        zlib1g-dev \
        librabbitmq-dev \
        libmcrypt-dev && \
    #
    # Install basic extensions \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install mysqli && \
    docker-php-ext-install pdo_pgsql && \
    docker-php-ext-install opcache && \
    docker-php-ext-install zip && \
    docker-php-ext-install bcmath && \
    docker-php-ext-install gmp && \
    docker-php-ext-install intl && \
    docker-php-ext-install sockets && \
    docker-php-ext-install sysvmsg && \
    docker-php-ext-install sysvsem && \
    docker-php-ext-install sysvshm && \
    docker-php-ext-install xmlrpc && \
    docker-php-ext-install gettext && \
    docker-php-ext-install pcntl && \
    docker-php-ext-install shmop && \
    #
    # Install gd extension
    docker-php-ext-configure gd \
        --with-jpeg-dir=/usr/lib \
        --with-freetype-dir=/usr/include/freetype2 && \
    docker-php-ext-install gd && \
    #
    # Install soap extension
    docker-php-ext-configure soap --enable-soap && \
    docker-php-ext-install soap && \
    #
    # Install other extension \
    pecl channel-update pecl.php.net && \
    pecl install mcrypt-1.0.2 && \
    pecl install amqp 1.9.4 && \
    pecl install redis-5.1.1 && \
    pecl install mongodb && \
    pecl install xhprof && \
    pecl install swoole-4.5.0 && \
    docker-php-ext-enable amqp redis mongodb xhprof swoole && \
    #
    # Install composer
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    #
    # Install PHP_CodeSniffer
    pear install PHP_CodeSniffer && \
    #
    # Configuration
    cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini && \
    #
    # Config timezone
    cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
    #
    # Clean up
    apt-get clean &&  \
    apt-get autoclean &&  \
    apt-get --purge -y autoremove &&  \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*