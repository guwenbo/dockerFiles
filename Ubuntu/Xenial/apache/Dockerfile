FROM ubuntu:16.04
LABEL author=guwenbo mail=bobo1314love@vip.qq.com
COPY bootstrap /usr/local/bin
RUN apt-get update && apt install -y apache2
EXPOSE 80 443
ENTRYPOINT ["bootstrap"]
