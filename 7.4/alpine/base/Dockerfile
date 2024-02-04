# hyperf/hyperf:7.4
#
# @link     https://www.hyperf.io
# @document https://hyperf.wiki
# @contact  group@hyperf.io
# @license  https://github.com/hyperf/hyperf/blob/master/LICENSE

ARG ALPINE_VERSION

FROM alpine:$ALPINE_VERSION

LABEL maintainer="Hyperf Developers <group@hyperf.io>" version="1.0" license="MIT"

ARG ALPINE_VERSION

# trust this project public key to trust the packages.
ADD https://alpine-apk-repository.knowyourself.cc/php-alpine.rsa.pub /etc/apk/keys/php-alpine.rsa.pub

##
# ---------- building ----------
##
RUN apk --update-cache add ca-certificates

# CONFIGURE ALPINE REPOSITORIES AND PHP BUILD DIR.
RUN echo "http://dl-cdn.alpinelinux.org/alpine/v${ALPINE_VERSION}/main" > /etc/apk/repositories && \
    echo "http://dl-cdn.alpinelinux.org/alpine/v${ALPINE_VERSION}/community" >> /etc/apk/repositories

RUN apk add --update-cache autoconf dpkg-dev dpkg file g++ gcc libc-dev make php7-dev php7-pear pkgconf re2c pcre-dev pcre2-dev zlib-dev libtool automake libaio-dev openssl-dev curl-dev  \
    php  libstdc++ openssl git bash libaio-dev openssl-dev curl-dev autoconf dpkg-dev dpkg file g++ gcc libc-dev make php7-dev php7-pear pkgconf re2c pcre-dev pcre2-dev zlib-dev libtool automake
RUN apk update
RUN set -ex \
     apk add --no-cache \
    # Install base packages ('ca-certificates' will install 'nghttp2-libs')
    ca-certificates \
    curl \
    wget \
    tar \
    xz \
    libressl \
    tzdata \
    pcre \
    php7 \
    php7-bcmath \
    php7-curl \
    php7-ctype \
    php7-dom \
    php7-gd \
    php7-iconv \
    php7-json \
    php7-mbstring \
    php7-mysqlnd \
    php7-openssl \
    php7-pdo \
    php7-pdo_mysql \
    php7-pdo_sqlite \
    php7-phar \
    php7-posix \
    php7-redis \
    php7-sockets \
    php7-sodium \
    php7-sysvshm \
    php7-sysvmsg \
    php7-sysvsem \
    php7-zip \
    php7-zlib \
    php7-xml \
    php7-xmlreader \
    php7-pcntl \
    php7-opcache    \
    && ln -sf /usr/bin/php7 /usr/bin/php \
    && apk del --purge *-dev \
    && rm -rf /var/cache/apk/* /tmp/* /usr/share/man /usr/share/php7 \
    && php -v \
    && php -m \
    && echo -e "\033[42;37m Build Completed :).\033[0m\n"
RUN apk add --no-cache --repository=http://dl-cdn.alpinelinux.org/alpine/v3.15/community/ php7-pecl-mongodb
#RUN pecl install mongodb
RUN  apk add --no-cache --repository=http://dl-cdn.alpinelinux.org/alpine/v3.15/community/ \
         curl \
         php7-dev \
         php7-iconv \
         php7-json \
         php7-curl \
         php7-openssl \
         php7-phar \
         php7-pcntl \
         php7-bcmath \
         php7-ctype \
         php7-dom \
         php7-gd \
         php7-mbstring \
         php7-mysqlnd \
         php7-pdo \
         php7-pdo_mysql \
         php7-pdo_sqlite \
         php7-posix \
         php7-redis \
         php7-sockets \
         php7-sodium \
         php7-sysvshm \
         php7-sysvmsg \
         php7-sysvsem \
         php7-zip \
         php7-zlib \
         php7-xml \
         php7-xmlreader\
         php7-xmlwriter \
         php7-opcache \
         php7-bz2 \
         php7-calendar \
         php7-event \
         php7-fileinfo \
         php7-ftp \
         php7-gettext \
         php7-intl \
        php7-mysqli \
         php7-shmop \
         php7-sqlite3 \
         php7-soap \
         php7-simplexml \
         php7-xsl \
         php7-tokenizer \
          php7-session

# update
RUN set -ex \
    && apk update \
    # for swoole extension libaio linux-headers
    && apk add --no-cache libstdc++ openssl git bash \
    && apk add --no-cache --virtual .build-deps $PHPIZE_DEPS libaio-dev openssl-dev curl-dev
