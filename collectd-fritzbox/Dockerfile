FROM ubuntu:18.04
  
LABEL maintainer="Knuppes"

ENV TIMEZONE=Europe/Berlin \
    DEBIAN_FRONTEND=noninteractive \
    CheckInterval=10 \
    InfluxDbIp=192.168.178.2 \
    InfluxDbCollectdPort=25826 \
    FritzBoxIp=192.168.178.1 \
    FritzBoxUser=collectd \
    FritzBoxPassword=mypassword

RUN apt-get update \
    && apt-get install -y python-pip \
    && apt-get install -y libxml2-dev \
    && apt-get install -y libxslt-dev \
    && apt-get install -y python-dev \
    && apt-get install -y zlib1g-dev \
    && pip2 install fritzcollectd

RUN apt-get install -y collectd

RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD collectd.conf /etc/collectd/collectd.conf
ADD start.sh /start.sh
RUN chmod +x /start.sh

ENV DEBUG=false

CMD ["/start.sh"]

