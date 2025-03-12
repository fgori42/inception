
    FROM alpine:3.20
    ARG PHP_VERSION=83 \
        DB_NAME \
        DB_USER \
        DB_PASS \
        DB_ROOT
    
    RUN apk update && apk upgrade && apk add --no-cache \
        php${PHP_VERSION} \
        php${PHP_VERSION}-fpm \
        php${PHP_VERSION}-mysqli \
        php${PHP_VERSION}-json \
        php${PHP_VERSION}-curl \
        php${PHP_VERSION}-exif \
        php${PHP_VERSION}-dom \
        php${PHP_VERSION}-exif \
        php${PHP_VERSION}-fileinfo \
        php${PHP_VERSION}-mbstring \
        php${PHP_VERSION}-openssl \
        php${PHP_VERSION}-xml \
        php${PHP_VERSION}-zip \
        php${PHP_VERSION}-redis \
        php${PHP_VERSION}-gd \
        php${PHP_VERSION}-dom \
        php${PHP_VERSION}-session \
        php${PHP_VERSION}-tokenizer \
        php${PHP_VERSION}-xmlwriter \
        php${PHP_VERSION}-simplexml \
        php${PHP_VERSION}-phar \
        php${PHP_VERSION}-ctype \
        php${PHP_VERSION}-iconv \
        php${PHP_VERSION}-intl \
        php${PHP_VERSION}-soap \
        php${PHP_VERSION}-xmlreader \
        php${PHP_VERSION}-posix \
        php${PHP_VERSION}-pdo \
        php${PHP_VERSION}-pdo_mysql \
        php${PHP_VERSION}-pdo_sqlite \
        php${PHP_VERSION}-sqlite3 \
        mysql-client \
        wget \
        unzip && \
        sed -i "s|listen = 127.0.0.1:9000|listen = 9000|g" \
          /etc/php83/php-fpm.d/www.conf && \
        sed -i "s|;listen.owner = nobody|listen.owner = nobody|g" \
          /etc/php83/php-fpm.d/www.conf && \
        sed -i "s|;listen.group = nobody|listen.group = nobody|g" \
          /etc/php83/php-fpm.d/www.conf && \
        rm -f /var/cache/apk/*
    WORKDIR /var/www
    RUN wget https://wordpress.org/latest.zip && \
        unzip latest.zip && \
        cp -rf wordpress/* . && \
        rm -rf wordpress latest.zip
    COPY ./requirements/wordpress/conf/wp-config-create.sh .
    RUN sh wp-config-create.sh && rm wp-config-create.sh && \
        chmod -R 0777 wp-content/
    CMD ["/usr/sbin/php-fpm83", "-F"]