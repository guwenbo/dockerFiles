FROM guwenbo/nginx:1.0
LABEL Author=gin \
      Mail=bobo1314love@vip.qq.com \
      Version=0.1
ENV PHP_VERSION 7.1.11
ENV PHP_PREFIX /usr/local/php
ENV ZABBIX_VERSION 3.4.4
RUN buildDeps="curl gcc make" ; \
    apt-get update && apt-get install -y --no-install-recommends libxml2-dev libjpeg-dev libpng-dev libfreetype6-dev libldap2-dev ; \
    ln -fs /usr/lib/x86_64-linux-gnu/*.so /usr/lib/ ; \
    apt-get update && apt-get install -y $buildDeps ; \
    curl -L http://cn2.php.net/get/php-${PHP_VERSION}.tar.gz/from/this/mirror | tar -xzv -f - -C ${SOURCE_DIR} ; \
    curl -L http://sourceforge.net/projects/zabbix/files/ZABBIX%20Latest%20Stable/${ZABBIX_VERSION}/zabbix-${ZABBIX_VERSION}.tar.gz/download | tar -xzv -f - -C ${SOURCE_DIR} ; \
    cd ${SOURCE_DIR}/php-${PHP_VERSION} \
    && ./configure --prefix=${PHP_PREFIX} \
                   --exec-prefix=${PHP_PREFIX} \
                   --enable-fpm \
                   --with-mysqli \
                   --with-ldap \
                   --enable-bcmath \
                   --enable-mbstring \
                   --enable-sockets \
                   --with-gd \
                   --with-jpeg-dir \
                   --with-png-dir \
                   --with-freetype-dir \
                   --with-gettext \
    && make \
    && make install ; \
    cp -a sapi/fpm/php-fpm /usr/local/sbin ; \
    apt-get purge -y --auto-remove  $buildDeps \
    && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y --no-install-recommends supervisor \
    && rm -rf /var/lib/apt/lists/*
COPY php.ini ${PHP_PREFIX}/lib
COPY php-fpm.conf ${PHP_PREFIX}/etc
COPY www.conf ${PHP_PREFIX}/etc/php-fpm.d
COPY nginx.conf /usr/local/nginx/conf
COPY start_php_fpm.conf /etc/supervisor/conf.d
COPY start_nginx.conf /etc/supervisor/conf.d
ENV PATH $PHP_PREFIX/bin:$PATH
EXPOSE 80
CMD ["supervisord","-n","-c","/etc/supervisor/supervisord.conf"]
