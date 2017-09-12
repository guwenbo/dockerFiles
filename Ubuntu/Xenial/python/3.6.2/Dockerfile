FROM ubuntu:16.04
RUN apt-get update && apt-get install -y gcc make zlib1g-dev libssl-dev libsqlite3-dev
ENV TARGET_FORDER=/usr/local/src
ADD https://www.python.org/ftp/python/3.6.2/Python-3.6.2.tar.xz $TARGET_FORDER
RUN apt-get install -y xz-utils
RUN cd $TARGET_FORDER \
    && tar xf Python-3.6.2.tar.xz \
    && cd Python-3.6.2 \
    && ./configure \
    && make \
    && make install
