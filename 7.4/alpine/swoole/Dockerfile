# hyperf/hyperf:7.4
#
# @link     https://www.hyperf.io
# @document https://hyperf.wiki
# @contact  group@hyperf.io
# @license  https://github.com/hyperf/hyperf/blob/master/LICENSE

ARG ALPINE_VERSION

FROM ghcr.io/shizeying/hyperf:7.4-alpine-v${ALPINE_VERSION}-base

LABEL maintainer="Hyperf Developers <group@hyperf.io>" version="1.0" license="MIT"

ARG SW_VERSION
ARG COMPOSER_VERSION

##
# ---------- env settings ----------
##
ENV SW_VERSION=${SW_VERSION:-"v4.8.11"} \
    COMPOSER_VERSION=${COMPOSER_VERSION:-"2.6.6"} \
    #  install and remove building packages
    PHPIZE_DEPS="autoconf dpkg-dev dpkg file g++ gcc libc-dev make php7-dev php7-pear pkgconf re2c pcre-dev pcre2-dev zlib-dev libtool automake"
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
#         php7-libxml \
#         php7-mongodb \
#         php7-pcre \
#         php7-Reflection \
#         php7-sdebug \
#         php7-standard \
#         php7-wxwork_finance_sdk \
#         php7-SPL \
#         php7-filter \
 #         php7-hash \
#         php7-igbinary \


ENV COMPOSER_ALLOW_SUPERUSER 1
RUN     cd /tmp \
        && curl -SL "https://github.com/swoole/swoole-src/archive/${SW_VERSION}.tar.gz" -o swoole.tar.gz \
        && ls -alh \
        # php extension:swoole
        && cd /tmp \
        && mkdir -p swoole \
        && tar -xf swoole.tar.gz -C swoole --strip-components=1 \
        && ln -s /usr/bin/phpize7 /usr/local/bin/phpize \
        && ln -s /usr/bin/php-config7 /usr/local/bin/php-config \
     && cd swoole \
      && phpize \
      && ./configure --enable-openssl --enable-http2 --enable-swoole-curl --enable-swoole-json \
      && make -s -j$(nproc) && make install \
         && echo "memory_limit=1G" > /etc/php7/conf.d/00_default.ini \
         && echo "opcache.enable_cli = 'On'" >> /etc/php7/conf.d/00_opcache.ini \
         && echo "extension=swoole.so" >> /etc/php7/conf.d/swoole.ini \
         && echo "swoole.use_shortname = 'Off'" >> /etc/php7/conf.d/50_swoole.ini \
         && php -v \
         && php -m \
         && php --ri swoole \
         && wget -nv -O /usr/local/bin/composer https://github.com/composer/composer/releases/download/${COMPOSER_VERSION}/composer.phar \
         && chmod u+x /usr/local/bin/composer \
         && composer  \
         && apk del .build-deps \
         && rm -rf /var/cache/apk/* /tmp/* /usr/share/man /usr/local/bin/php* \
          && echo -e "\033[42;37m Build Completed :).\033[0m\n"
