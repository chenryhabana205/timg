FROM grafana/grafana:6.7.1-ubuntu
MAINTAINER Mateusz Trojak <mateusz.trojak@gmail.com>
LABEL version="1.2"
LABEL description="Grafana docker image with custom setup"

USER root

RUN apt-get -q update &&\
    DEBIAN_FRONTEND="noninteractive" apt-get -q upgrade -y -o Dpkg::Options::="--force-confnew" --no-install-recommends &&\
    DEBIAN_FRONTEND="noninteractive" apt-get -q install -y -o Dpkg::Options::="--force-confnew" --no-install-recommends curl gosu &&\
    apt-get -q autoremove &&\
    apt-get -q clean -y && rm -rf /var/lib/apt/lists/* && rm -f /var/cache/apt/*.bin

ADD run.sh /run.sh
RUN chmod +x /run.sh
RUN mkdir -p /opt/grafana/dashboards
ADD ["*.json", "/opt/grafana/dashboards/"]
ADD ["default-dashboard.yaml", "/etc/grafana/provisioning/dashboards/"]

COPY preplugins.sh /root/
RUN chmod +x /root/preplugins.sh
RUN /root/preplugins.sh

CMD ["/run.sh"]
