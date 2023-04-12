FROM ubuntu:18.04 as build

ENV DEBIAN_FRONTEND=noninteractive

COPY install /install
RUN /install

COPY build_openssl /build_openssl
RUN /build_openssl

COPY build_mysql /build_mysql
RUN /build_mysql

COPY Banner.cpp /Banner.cpp
COPY build_ashamane /build_ashamane
RUN /build_ashamane

FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update -yq && \
    apt-get install -yq libatomic1 libreadline7 libboost-system1.65.1 libboost-filesystem1.65.1 libboost-program-options1.65.1 libboost-iostreams1.65.1 libboost-thread1.65.1 && \
    rm -rf /var/lib/apt/lists/*
RUN mkdir /usr/local/logs
COPY --from=build /AshamaneCore /AshamaneCore
COPY --from=build /usr/local /usr/local
COPY extract /usr/local/bin/extract
