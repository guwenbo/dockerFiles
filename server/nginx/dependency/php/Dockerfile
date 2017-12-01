FROM guwenbo/nginx:1.0
LABEL Author=gin \
      Mail=bobo1314love@vip.qq.com \
      Version=0.1
ENV PHP_VERSION 7.1.11
ENV PHP_TAR_BALL=php-${PHP_VERSION}.tar.gz
ENV PHP_PREFIX /usr/local/php
RUN buildDeps="wget gcc make" ; \
    apt-get update && apt-get install -y --no-install-recommends libxml2-dev ; \
    apt-get update && apt-get install -y $buildDeps ; \
    wget -O ${PHP_TAR_BALL} http://cn2.php.net/get/${PHP_TAR_BALL}/from/this/mirror ; \
    tar -xzv -f ${PHP_TAR_BALL} -C ${SOURCE_DIR} ; \
    rm ${PHP_TAR_BALL} ; \
    cd ${SOURCE_DIR}/php-${PHP_VERSION} \
    && ./configure --prefix=${PHP_PREFIX} \
                   --exec-prefix=${PHP_PREFIX} \
                   --enable-fpm \
                   --with-mysqli \
    && make \
    && make install ; \
    cp -a php.ini-development ${PHP_PREFIX}/lib/php.ini ; \
    cp -a ${PHP_PREFIX}/etc/php-fpm.conf.default ${PHP_PREFIX}/etc/php-fpm.conf ; \
    cp -a sapi/fpm/php-fpm /usr/local/bin ; \
    cp -a ${PHP_PREFIX}/etc/php-fpm.d/www.conf.default ${PHP_PREFIX}/etc/php-fpm.d/www.conf ; \
    sed -i '/^;cgi.fix_pathinfo=*/c\cgi.fix_pathinfo=0' ${PHP_PREFIX}/lib/php.ini ; \
    sed -i -e '/^user =*/c\user = www-data' -e '/^group =*/c\group = www-data' ${PHP_PREFIX}/etc/php-fpm.d/www.conf ; \
    apt-get purge -y --auto-remove  $buildDeps \
    && rm -rf /var/lib/apt/lists/*
ENV PATH $PHP_PREFIX/bin:$PATH
RUN apt-get update && apt-get install -y --no-install-recommends supervisor \
    && rm -rf /var/lib/apt/lists/*
RUN echo "[program:php-fpm]\ncommand=php-fpm" > /etc/supervisor/conf.d/php-fpm.conf; \
    echo "[program:nginx]\ncommand=nginx" > /etc/supervisor/conf.d/nginx.conf
ENV ZABBIX_VERSION 3.4.4
RUN apt-get update && apt-get install -y curl ; \
    curl -L http://sourceforge.net/projects/zabbix/files/ZABBIX%20Latest%20Stable/${ZABBIX_VERSION}/zabbix-${ZABBIX_VERSION}.tar.gz/download | tar -xzv -f - -C ${SOURCE_DIR} ; \
    apt-get purge -y --auto-remove  curl \
    && rm -rf /var/lib/apt/lists/*
COPY nginx.conf /usr/local/nginx/conf
EXPOSE 80
CMD ["supervisord","-n","-c","/etc/supervisor/supervisord.conf"]
