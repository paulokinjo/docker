FROM paulokinjo/ssh

LABEL maintainer="paulokinjo@hotmail.com"

ENV PROMETHEUS_VERSION="2.18.1"
ENV PROMETHEUS_URL="https://github.com/prometheus/prometheus/releases/download" \
  PROMETHEUS_PACKAGE_EXT=".tar.gz" \
  PROMETHEUS_PACKAGE="prometheus-${PROMETHEUS_VERSION}.linux-amd64" \
  WORK_PATH=/usr/src/monitoring/prometheus

WORKDIR ${WORK_PATH}

RUN wget ${PROMETHEUS_URL}/v${PROMETHEUS_VERSION}/${PROMETHEUS_PACKAGE}${PROMETHEUS_PACKAGE_EXT} \
  && tar -xzvf ${PROMETHEUS_PACKAGE}${PROMETHEUS_PACKAGE_EXT} \
  && cp -R ${WORK_PATH}/${PROMETHEUS_PACKAGE}/* ./

# if you just want to start prometheus as root
#./prometheus --config.file=prometheus.yml

# create user
RUN useradd --no-create-home --shell /bin/false prometheus \
  && mkdir -p /etc/prometheus \
  && mkdir -p /var/lib/prometheus

# set ownership
RUN chown prometheus:prometheus /etc/prometheus \
  && chown prometheus:prometheus /var/lib/prometheus

# copy binaries
RUN cp prometheus /usr/local/bin/ \
  && cp promtool /usr/local/bin/ \
  && chown prometheus:prometheus /usr/local/bin/prometheus \
  && chown prometheus:prometheus /usr/local/bin/promtool

# copy config
RUN cp -r consoles /etc/prometheus \
  && cp -r console_libraries /etc/prometheus \
  && cp prometheus.yml /etc/prometheus/prometheus.yml \
  && chown -R prometheus:prometheus /etc/prometheus/consoles \
  && chown -R prometheus:prometheus /etc/prometheus/console_libraries

# default command
COPY ./supervisor.conf .
RUN cat ./supervisor.conf >> /etc/supervisor.conf
CMD ["supervisord", "-c", "/etc/supervisor.conf"]

