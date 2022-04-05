FROM python:alpine
# RUN echo 'http://dl-cdn.alpinelinux.org/alpine/v3.9/main' >> /etc/apk/repositories
# RUN echo 'http://dl-cdn.alpinelinux.org/alpine/v3.9/community' >> /etc/apk/repositories
# RUN apk upgrade --update

RUN apk add openjdk8-jre git alpine-sdk linux-headers bsd-compat-headers openssl-dev xz-dev curl-dev

RUN git clone https://github.com/mongodb/mongo.git

WORKDIR mongo
RUN python3 -m pip install -r etc/pip/compile-requirements.txt
RUN python3 buildscripts/scons.py DESTDIR=/opt/mongo install-mongod

RUN adduser -D -H -h /srv/unifi unifi

WORKDIR /srv

RUN wget http://www.ubnt.com/downloads/unifi/7.0.25/UniFi.unix.zip; unzip UniFi.unix.zip
RUN mv UniFi unifi; chown -R unifi:unifi unifi; chmod o-rwx unifi

RUN cd /srv/unifi/bin; rm mongod; ln -s /usr/bin/mongod
RUN mkdir -p /etc/unifi/log

COPY unifi-run /etc/unifi/run
COPY unifi-log-run /etc/unifi/log/run

RUN adduser -D -H -h /var/log log
RUN mkdir -p /var/log/unifi

RUN chown log:log /var/log/unifi
RUN chmod 750 /var/log/unifi

COPY initd-unifi /etc/init.d/unifi
# RUN rc-service unifi start
RUN rc-update add unifi boot

COPY unifi-backup /usr/local/bin/unifi-backup
