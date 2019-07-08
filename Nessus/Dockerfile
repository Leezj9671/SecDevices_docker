FROM ubuntu:18.10
MAINTAINER TEST

USER root
#VOLUME ["/opt/nessus"]

#按版本号自行修改
COPY all-2.0.tar.gz /root/
COPY Nessus-8.2.3-debian6_amd64.deb /root/
COPY nessus.zip /root/

WORKDIR /root
RUN apt-get update -y && apt-get install -y unzip &&  unzip nessus.zip \
  && dpkg -i Nessus-8.2.3-debian6_amd64.deb \
  && cp ./conf/nessus-fetch.db /opt/nessus/etc/nessus \
  && cp -frap ./nessus/* /opt/nessus/var/nessus \
  && /opt/nessus/sbin/nessuscli update all-2.0.tar.gz

EXPOSE 8834
CMD /opt/nessus/sbin/nessus-service
