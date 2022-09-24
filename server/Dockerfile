FROM ubuntu:20.04

#ARG repository="deb http://repo.yandex.ru/clickhouse/deb/stable/ main/"
ARG version=22.8.4.7
ARG gosu_ver=1.10

RUN apt-get update \
    && apt-get install --yes --no-install-recommends \
        apt-transport-https \
        dirmngr \
        gnupg \
        wget \
    && mkdir -p /etc/apt/sources.list.d \
	&& wget  --no-check-certificate https://github.com/ClickHouse/ClickHouse/releases/download/v${version}-lts/clickhouse-server_${version}_amd64.deb \
	&& wget  --no-check-certificate https://github.com/ClickHouse/ClickHouse/releases/download/v${version}-lts/clickhouse-common-static_${version}_amd64.deb \
	&& wget  --no-check-certificate https://github.com/ClickHouse/ClickHouse/releases/download/v${version}-lts/clickhouse-client_${version}_amd64.deb \
    && env DEBIAN_FRONTEND=noninteractive \
        apt-get install --allow-unauthenticated --yes --no-install-recommends \
            libgcc-7-dev \
            locales \
            curl \
            netcat \
            tzdata \
            jq \
			./clickhouse-common-static_${version}_amd64.deb \
			./clickhouse-client_${version}_amd64.deb \
			./clickhouse-server_${version}_amd64.deb \
    && rm -rf \
        /var/lib/apt/lists/* \
        /var/cache/debconf \
        /tmp/* \
		./clickhouse-* \
    && apt-get clean

ADD https://github.com/tianon/gosu/releases/download/1.10/gosu-amd64 /bin/gosu

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN mkdir /docker-entrypoint-initdb.d

COPY docker_related_config.xml /etc/clickhouse-server/config.d/
COPY entrypoint.sh /entrypoint.sh

RUN chmod +x \
    /entrypoint.sh \
    /bin/gosu

EXPOSE 9000 8123 9009
VOLUME /var/lib/clickhouse

ENV CLICKHOUSE_CONFIG /etc/clickhouse-server/config.xml

ENTRYPOINT ["/entrypoint.sh"]
