FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update -yq
RUN apt-get install -yq git clang cmake make gcc g++ libbz2-dev libreadline-dev libncurses-dev libboost-all-dev p7zip
RUN update-alternatives --install /usr/bin/cc cc /usr/bin/clang 100
RUN update-alternatives --install /usr/bin/c++ c++ /usr/bin/clang 100

RUN apt-get install -yq curl
RUN cd /root && curl https://www.openssl.org/source/openssl-1.0.2s.tar.gz > openssl-1.0.2s.tar.gz
RUN cd /root && tar xvfz openssl-1.0.2s.tar.gz
RUN cd /root/openssl-1.0.2s && ./config shared --prefix=/usr/local/ssl && make -j 16 && make install

RUN apt-get install -yq wget
RUN cd /root && wget https://dev.mysql.com/get/Downloads/MySQL-5.6/mysql-5.7.41.tar.gz
RUN cd /root && tar xvfz mysql-5.7.41.tar.gz
RUN cd /root/mysql-5.7.41 && rm /usr/local/ssl/lib/*.a
RUN cd /root/mysql-5.7.41 && sed -i 's/IF(NOT BOOST_MINOR_VERSION EQUAL 59)/IF(NOT BOOST_MINOR_VERSION EQUAL 65)/' cmake/boost.cmake
RUN cd /root/mysql-5.7.41 && cmake -DWITHOUT_SERVER=ON -DWITH_SSL=/usr/local/ssl -DOPENSSL_INCLUDE_DIR=/usr/local/ssl/include .
RUN cd /root/mysql-5.7.41 && make -j 16 && make install

# RUN cd /root && git clone -b TDB735.00 --depth 1 https://github.com/TrinityCore/TrinityCore.git
RUN cd /root && git clone -b legion --depth 1 https://github.com/AshamaneProject/AshamaneCore
COPY Banner.cpp /root/AshamaneCore/src/common/Banner.cpp
RUN cd /root/AshamaneCore && mkdir build && cd build && cmake -DOPENSSL_SSL_LIBRARIES=/usr/local/ssl/lib/libssl.so -DOPENSSL_CRYPTO_LIBRARIES=/usr/local/ssl/lib/libcrypto.so -DOPENSSL_INCLUDE_DIR=/usr/local/ssl/include ../ && make -j 16 && make install

RUN mkdir /usr/local/logs

# RUN wget https://github.com/TrinityCore/TrinityCore/releases/download/TDB735.00/TDB_full_735.00_2018_02_19.7z -O /root/tdb.7z
RUN wget https://github.com/AshamaneProject/AshamaneCore/releases/download/ADB_735.00/ADB_735.00.zip -O /root/ac.zip
RUN apt-get install -yq unzip
RUN cd /root && unzip ac.zip
RUN mv /root/*.sql /usr/local/bin/

RUN rm /root/mysql-5.7.41.tar.gz
RUN rm /root/openssl-1.0.2s.tar.gz
RUN rm -rf /root/mysql-5.7.41
RUN rm -rf /root/openssl-1.0.2s
RUN rm -rf /root/ac.zip
RUN rm -rf /root/AshamaneCore/build

COPY extract /usr/local/bin/extract
