FROM debian:jessie
MAINTAINER Aleksandr Savin <f0x.asavin@gmail.com>

RUN groupadd -r mongodb && useradd -r -g mongodb mongodb
RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
		numactl \
	&& rm -rf /var/lib/apt/lists/*

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927

ENV MONGO_MAJOR stable
ENV MONGO_VERSION 3.2.8

RUN echo "deb http://repo.mongodb.org/apt/debian jessie/mongodb-org/$MONGO_MAJOR main" > /etc/apt/sources.list.d/mongodb-org.list

RUN set -x \
	&& apt-get update \
	&& apt-get install -y \
		mongodb-org=$MONGO_VERSION \
		mongodb-org-server=$MONGO_VERSION \
		mongodb-org-shell=$MONGO_VERSION \
		mongodb-org-mongos=$MONGO_VERSION \
		mongodb-org-tools=$MONGO_VERSION \
	&& rm -rf /var/lib/apt/lists/* 

WORKDIR /data
VOLUME /data/db 

ENTRYPOINT ["/usr/bin/mongod"]

EXPOSE 27017
