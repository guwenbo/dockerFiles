FROM guwenbo/apache:1.0
RUN yum install -y libxml2 libxml2-devel libjpeg-devel libpng-devel freetype-devel openldap-devel
ENV TARGET_DIR=/usr/local/src
ADD php-7.1.8.tar.gz $TARGET_DIR
RUN cd $TARGET_DIR/php-7.1.8 && ./configure --prefix=/usr/local/php \
            --with-apxs2=/usr/local/apache2/bin/apxs \
            --with-config-file-path=/usr/local/php/lib \
            --with-mysqli \
            --with-pdo-mysql \
            --enable-bcmath \
            --enable-mbstring \
            --enable-sockets \
            --enable-json \
            --enable-zip \
            --enable-ftp \
            --enable-session \
            --enable-fpm \
            --enable-soap \
            --with-gettext \
            --with-gd \
            --with-jpeg-dir \
            --with-png-dir \
            --with-freetype-dir && make && make install
RUN cd $TARGET_DIR/php-7.1.8 && cp php.ini-development /usr/local/php/lib/php.ini
RUN sed -i '$a <FilesMatch \.php$> \n SetHandler application/x-httpd-php \n</FilesMatch>' /usr/local/apache2/conf/httpd.conf
