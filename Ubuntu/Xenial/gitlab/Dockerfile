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
    && tar -zxf git-2.14.1.tar.gz \
    && cd git-2.14.1 \
    && ./configure \
    && make prefix=/usr/local all \
    && make prefix=/usr/local install
# install ruby from source
RUN cd /tmp \
    && curl -O --progress https://cache.ruby-lang.org/pub/ruby/2.3/ruby-2.3.3.tar.gz \
    && tar -zxf ruby-2.3.3.tar.gz \
    && cd ruby-2.3.3 \
    && ./configure --disable-install-rdoc \
    && make \
    && make install \
    && gem install bundler --no-ri --no-rdoc
# install GO
RUN cd /tmp \
    && curl -O --progress https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz \
    && tar -C /usr/local -xzf go1.8.3.linux-amd64.tar.gz \
    && ln -sf /usr/local/go/bin/go /usr/local/bin/go \
    && ln -sf /usr/local/go/bin/godoc /usr/local/bin/godoc \
    && ln -sf /usr/local/go/bin/gofmt /usr/local/bin/gofmt
# Node and yarn
# install node v7.x
# curl --location 向curl加入允许重定向功能
RUN curl --location https://deb.nodesource.com/setup_7.x | bash - \
    && apt-get install -y nodejs
# install yarn
RUN curl --silent --show-error https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update -y \
    && apt-get install -y yarn
# add user for gitlab
RUN adduser --disabled-login --gecos 'gitlab' git
