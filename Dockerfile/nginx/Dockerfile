# Nginx Version
ARG NGINX_VERSION=1.21.4

# The Base Image
FROM nginx:${NGINX_VERSION}-alpine

# The Maintainer
MAINTAINER JohnHe China <564079964@qq.com>

# Time Zone
ENV TIME_ZONE=Asia/Shanghai

# Running required command
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories && \
    apk update && \
    apk add --no-cache --virtual .build-deps \
    make net-tools pcre pcre-dev perl-dev zlib zlib-dev geoip geoip-dev gd gd-dev libxslt libxslt-dev openssl openssl-dev gcc g++ && \
    wget http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz && \
    tar zxvf nginx-${NGINX_VERSION}.tar.gz && \
    rm nginx-${NGINX_VERSION}.tar.gz && \
    cd nginx-${NGINX_VERSION} && \
    ./configure --prefix=/etc/nginx \
                --sbin-path=/usr/sbin/nginx \
                --modules-path=/usr/lib/nginx/modules \
                --conf-path=/etc/nginx/nginx.conf \
                --error-log-path=/var/log/nginx/error.log \
                --http-log-path=/var/log/nginx/access.log \
                --pid-path=/var/run/nginx.pid \
                --lock-path=/var/run/nginx.lock \
                --with-http_xslt_module \
                --with-http_image_filter_module \
                --with-http_geoip_module \
                --with-http_degradation_module \
                --with-http_perl_module && make && \
    apk del .build-deps && \
    #
    # Clean up
    rm -rf /var/cache/apk/*  /tmp/* ../nginx-${NGINX_VERSION} && \
    cp /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime