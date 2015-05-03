# Pull base image
FROM java:8
MAINTAINER Emmanuel COQUELIN <ecoquelin@esensconsulting.com>	

# Set install version
ENV ES_PKG_NAME elasticsearch-1.5.2

# Install environment
RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get -y install curl wget supervisor cron


# Install elasticsearch
WORKDIR /opt
RUN wget --no-check-certificate -O- https://download.elastic.co/elasticsearch/elasticsearch/$ES_PKG_NAME.tar.gz | tar xvfz -
RUN mv $ES_PKG_NAME elasticsearch

ENV ES_CLUSTER_NAME elasticsearch

EXPOSE 9200 9300

ADD supervisord.conf /etc/supervisor/conf.d/elasticsearch.conf

ADD run ./run
RUN chmod +x ./run
CMD ./run
