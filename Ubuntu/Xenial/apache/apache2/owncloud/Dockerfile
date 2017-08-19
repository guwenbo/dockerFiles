FROM ubuntu:16.04
LABEL author=guwenbo version=1.0 mail=bobo1314love@vip.qq.com
RUN apt-get update && apt-get install -y curl apt-transport-https
RUN curl https://download.owncloud.org/download/repositories/stable/Ubuntu_16.04/Release.key | apt-key add - \
&& echo 'deb https://download.owncloud.org/download/repositories/stable/Ubuntu_16.04/ /' | tee /etc/apt/sources.list.d/owncloud.list \
&& apt-get update \
&& apt-get install -y owncloud
COPY bootstrap /usr/local/sbin
ENTRYPOINT ["bootstrap"]
