FROM ubuntu:16.04
LABEL author=guwenbo mail=bobo1314love@vip.qq.com
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y sudo \
                          curl \
                          build-essential \
                          zlib1g-dev \
                          libyaml-dev \
                          libssl-dev \
                          libgdbm-dev \
                          libre2-dev \
                          libreadline-dev \
                          libncurses5-dev \
                          libffi-dev \
                          openssh-server \
                          checkinstall \
                          libxml2-dev \
                          libxslt-dev \
                          libcurl4-openssl-dev \
                          libicu-dev \
                          logrotate \
                          python-docutils \
                          pkg-config \
                          cmake
# Make sure Git is version 2.13.0 or higher
RUN apt-get install -y libexpat1-dev \
                       gettext \
                       libz-dev \
    && cd /tmp \
    && curl -O --progress https://www.kernel.org/pub/software/scm/git/git-2.14.1.tar.gz \
    && tar -xzf git-2.14.1.tar.gz \
    && cd git-2.14.1 \
    && ./configure \
    && make prefix=/usr/local all \
    && make prefix=/usr/local install
