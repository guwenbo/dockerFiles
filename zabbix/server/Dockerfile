FROM debian:jessie-backports
LABEL Author=gin \
      Mail=bobo1314love@vip.qq.com \
      Version=0.1
ENV SOURCE_DIR /usr/local/src
ENV ZABBIX_VERSION 3.4.4
RUN buildDeps="curl gcc make" ; \
    apt-get update && apt-get install -y $buildDeps ; \
    apt-get install -y --no-install-recommends libmysqlclient-dev libsnmp-dev libssh2-1-dev libpcre3-dev libevent-dev ; \
    curl -L http://sourceforge.net/projects/zabbix/files/ZABBIX%20Latest%20Stable/${ZABBIX_VERSION}/zabbix-${ZABBIX_VERSION}.tar.gz/download | tar -xzv -f - -C ${SOURCE_DIR} ; \
    cd ${SOURCE_DIR}/zabbix-${ZABBIX_VERSION} \
    && ./configure --prefix=/usr/local/zabbix --exec-prefix=/usr/local/zabbix --enable-server --with-net-snmp --with-mysql --with-ssh2 \
    && make \
    && make install ; \
    apt-get purge -y --auto-remove  $buildDeps \
    && rm -rf /var/lib/apt/lists/*
RUN groupadd zabbix ; \
    useradd -g zabbix zabbix
