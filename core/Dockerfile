FROM ubuntu:18.04 as builder

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

RUN mkdir /usr/local/logs
COPY install_runtime /install_runtime
RUN /install_runtime
COPY --from=builder /AshamaneCore /AshamaneCore
COPY --from=builder /usr/local /usr/local
COPY extract /usr/local/bin/extract
