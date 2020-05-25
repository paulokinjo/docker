FROM paulokinjo/ssh

LABEL maintainer="paulokinjo@hotmail.com"

RUN apt-get install -y apt-transport-https \
  software-properties-common

RUN wget -q -O - https://packages.grafana.com/gpg.key | apt-key add - \
  # Alternatively you can add the beta repository, see in the table above \
  && add-apt-repository "deb https://packages.grafana.com/oss/deb stable main" 

RUN apt-get update \
  && apt-get install -y grafana

# # default command
COPY ./supervisor.conf .
RUN cat ./supervisor.conf >> /etc/supervisor.conf
CMD ["supervisord", "-c", "/etc/supervisor.conf"]

