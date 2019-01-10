FROM debian:stretch

LABEL maintainer="Jorge Matricali <jorgematricali@gmail.com>"

RUN apt-get update && apt-get -y install wget
RUN wget https://repo.mongodb.org/apt/debian/dists/stretch/mongodb-org/4.0/main/binary-amd64/mongodb-org-mongos_4.0.5_amd64.deb
RUN dpkg -i mongodb-org-mongos_4.0.5_amd64.deb && rm mongodb-org-mongos_4.0.5_amd64.deb

RUN mkdir -p /var/log/mongos /etc/mongos
COPY ./etc/mongos/mongos.conf /etc/mongos/mongos.conf
COPY ./etc/mongos/mongos.keyfile /etc/mongos/mongos.keyfile
RUN chmod 600 /etc/mongos/mongos.keyfile

RUN ln -sf /dev/stdout /var/log/mongos/mongos.log

EXPOSE 27200

STOPSIGNAL SIGTERM
CMD ["/usr/bin/mongos", "-f", "/etc/mongos/mongos.conf"]
