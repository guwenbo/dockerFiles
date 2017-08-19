FROM ubuntu:16.04
LABEL author=gin mail=bobo1314love@vip.qq.com
COPY redis-4.0.0 /opt/redis-4.0.0
RUN cp -s /opt/redis-4.0.0/src/redis-server /usr/local/bin/redis-server && cp -s /opt/redis-4.0.0/src/redis-cli /usr/local/bin/redis-cli
VOLUME /config/
