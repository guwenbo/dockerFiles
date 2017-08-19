FROM ubuntu:16.04
LABEL author=guwenbo mail=bobo1314love@vip.qq.com
ENV TOMCAT_PACKAGE=apache-tomcat-9.0.0.M26.tar.gz JDK_PACKAGE=jdk-8u144-linux-x64.tar.gz
ADD $TOMCAT_PACKAGE /usr/local/
ADD $JDK_PACKAGE /usr/local/
RUN update-alternatives --install /usr/bin/java java /usr/local/jdk1.8.0_144/bin/java 1001
ENTRYPOINT ["/usr/local/apache-tomcat-9.0.0.M26/bin/catalina.sh","run"]
