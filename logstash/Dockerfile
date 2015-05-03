FROM ubuntu:utopic
MAINTAINER Emmanuel COQUELIN <ecoquelin@esensconsulting.com>

ENV DEBIAN_FRONTEND noninteractive
ENV LOGSTASH_VER 1.5.0-rc3
WORKDIR /opt

# Dependencies
RUN apt-get update -qq
RUN apt-get install -y -qq wget python openjdk-7-jre-headless

# Install Logstash

RUN wget --quiet "https://download.elastic.co/logstash/logstash/logstash-$LOGSTASH_VER.tar.gz" -O "/opt/logstash-$LOGSTASH_VER.tar.gz" --no-check-certificate
RUN tar -zxf logstash-$LOGSTASH_VER.tar.gz
RUN mv logstash-$LOGSTASH_VER logstash

# Install plugins

# Config files
ADD server.conf /etc/logstash/server.conf
ADD logstash-forwarder.key /etc/logstash/logstash-forwarder.key
ADD logstash-forwarder.crt /etc/logstash/logstash-forwarder.crt

# Exposing ports

CMD /opt/logstash/bin/logstash -f /etc/logstash/server.conf
