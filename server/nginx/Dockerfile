FROM debian:jessie-backports
LABEL Author=gin \
      Mail=bobo1314love@vip.qq.com \
      Version=0.1
ENV SOURCE_DIR /usr/local/src
ENV PCRE_VERSION 8.41
ENV ZLIB_VERSION 1.2.11
ENV NGINX_VERSION 1.13.6
RUN buildDeps="curl gcc g++ make" ; \
    apt-get update && apt-get install -y $buildDeps ; \
    curl https://ftp.pcre.org/pub/pcre/pcre-${PCRE_VERSION}.tar.gz | tar -xzv -f - -C $SOURCE_DIR ; \
    curl http://www.zlib.net/zlib-${ZLIB_VERSION}.tar.gz | tar -xzv -f - -C $SOURCE_DIR ; \
    curl http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz | tar -xzv -f - -C $SOURCE_DIR ; \
    cd ${SOURCE_DIR}/nginx-${NGINX_VERSION} \
    && ./configure \
        --with-pcre=${SOURCE_DIR}/pcre-${PCRE_VERSION} \
        --with-zlib=${SOURCE_DIR}/zlib-${ZLIB_VERSION} \
    && make \
    && make install ; \
    apt-get purge -y --auto-remove  $buildDeps \
    && rm -rf /var/lib/apt/lists/*
ENV PATH /usr/local/nginx/sbin:$PATH
CMD ["nginx","-g","daemon off;"]
