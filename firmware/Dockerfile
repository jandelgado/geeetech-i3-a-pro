FROM ubuntu:18.04
LABEL maintainer "Jan Delgado <jdelgado@gmx.net>"

RUN apt-get update \
     && apt-get install -y  python3 python3-pip \
     && rm -rf /var/cache/apk/*  \
     && mkdir /marlin

RUN pip3 install platformio

ADD https://github.com/tianon/gosu/releases/download/1.11/gosu-amd64 /usr/local/bin/gosu
ADD etc/entrypoint.sh /etc
RUN chmod 755 /etc/entrypoint.sh /usr/local/bin/gosu

ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8
ENV HOME=/marlin

WORKDIR "/marlin"
ENTRYPOINT ["/etc/entrypoint.sh"]
CMD ["/bin/bash"]

