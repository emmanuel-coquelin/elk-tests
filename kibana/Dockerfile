FROM ubuntu:14.04
MAINTAINER Emmanuel COQUELIN <ecoquelin@esensconsulting.com>

# Set Installation variables
ENV KIBANA_VER 4.0.2

# Dependencies
RUN apt-get update -qq
RUN sudo apt-get install -y -qq nginx-full wget vim

# Kibana
WORKDIR /opt
RUN wget --no-check-certificate -O- "https://download.elastic.co/kibana/kibana/kibana-$KIBANA_VER-linux-x64.tar.gz" | tar zvxf -
RUN mkdir /etc/kibana # This is where the htpasswd file is placed by the run scrip

ADD kibana /etc/nginx/sites-available/kibana
ADD kibana-secure /etc/nginx/sites-available/kibana-secure
RUN rm /etc/ngix/sites-enabled/*
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

ENV KIBANA_SECURE true
ENV KIBANA_USER kibana
ENV KIBANA_PASSWORD kibana

# Exposing ports
EXPOSE 5601

ADD supervisord.conf /etc/supervisor/conf.d/kibana.conf

ADD run ./run
RUN chmod +x ./run
CMD ./run
