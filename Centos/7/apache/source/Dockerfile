FROM guwenbo/centos_base:1.0
LABEL author=gin mail=bobo1314love@vip.qq.com
RUN yum install -y gcc make gcc-c++ expat-devel vim sudo
ENV TARGET_DIR /usr/local/src
ADD apr-1.6.2.tar.gz $TARGET_DIR
RUN cd $TARGET_DIR/apr-1.6.2 && ./configure --prefix=/usr/local/apr && make && make install
ADD apr-util-1.6.0.tar.gz $TARGET_DIR
RUN cd $TARGET_DIR/apr-util-1.6.0 && ./configure --prefix=/usr/local/apr-util --with-apr=/usr/local/apr && make && make install
ADD pcre-8.41.tar.gz $TARGET_DIR
RUN cd $TARGET_DIR/pcre-8.41 && ./configure --prefix=/usr/local/pcre && make && make install
ADD openssl-1.0.2l.tar.gz $TARGET_DIR
RUN cd $TARGET_DIR/openssl-1.0.2l && ./config --prefix=/usr/local/openssl -fPIC && make depend && make install
ADD httpd-2.4.27.tar.gz $TARGET_DIR
RUN cd $TARGET_DIR/httpd-2.4.27 && ./configure --prefix=/usr/local/apache2 --with-apr=/usr/local/apr --with-apr-util=/usr/local/apr-util --with-pcre=/usr/local/pcre --with-ssl=/usr/local/openssl --enable-ssl --enable-so && make && make install
