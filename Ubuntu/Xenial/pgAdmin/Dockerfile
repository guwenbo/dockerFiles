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
ADD https://bootstrap.pypa.io/get-pip.py $TARGET_FORDER
RUN python3 $TARGET_FORDER/get-pip.py
ADD https://ftp.postgresql.org/pub/pgadmin/pgadmin4/v1.6/pip/pgadmin4-1.6-py2.py3-none-any.whl $TARGET_FORDER
RUN pip3.6 install $TARGET_FORDER/pgadmin4-1.6-py2.py3-none-any.whl
RUN sed -i "s/'127.0.0.1'/'0.0.0.0'/" /usr/local/lib/python3.6/site-packages/pgadmin4/config.py
ENV PGADMIN_SETUP_EMAIL=bobo1314love@vip.qq.com PGADMIN_SETUP_PASSWORD=abcd@1234
COPY bootstrap.sh /usr/local/bin/
EXPOSE 5050
ENTRYPOINT ["bootstrap.sh"]
