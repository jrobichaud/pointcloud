FROM postgres:9.6

ENV POSTGRES_VERSION 9.6
ENV POSTGIS_VERSION 2.3

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        postgis \
        postgresql-${POSTGRES_VERSION}-postgis-${POSTGIS_VERSION} \
        postgresql-${POSTGRES_VERSION}-postgis-${POSTGIS_VERSION}-scripts

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        git \
        ca-certificates \
        build-essential \
        cmake \
        autoconf \
        automake \
        zlib1g-dev \
        postgresql-server-dev-${POSTGRES_VERSION} \
        libxml2-dev \
    && rm -rf /var/lib/apt/lists/* \
    && git clone https://github.com/verma/laz-perf.git \
    && cd laz-perf \
    && cmake . \
    && make \
    && make install \
    && cd / \
    && git clone https://github.com/pgpointcloud/pointcloud \
    && cd pointcloud \
    && ./autogen.sh \
    && ./configure CFLAGS="-Wall -Werror -O2 -g" --with-lazperf=/usr/local \
    && make \
    && make install \
    && apt-get purge -y --auto-remove \
        git \
        ca-certificates \
        build-essential \
        cmake \
        autoconf \
        automake \
        zlib1g-dev \
        postgresql-server-dev-${POSTGRES_VERSION}  \
        libxml2-dev
