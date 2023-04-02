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

# NOTE: Maybe this core is more useful: https://github.com/AshamaneProject/AshamaneCore/releases/tag/ADB_735.10
RUN cd /root && git clone -b TDB735.00 --depth 1 https://github.com/TrinityCore/TrinityCore.git
COPY Banner.cpp /root/TrinityCore/src/common/Banner.cpp
RUN cd /root/TrinityCore && mkdir build && cd build && cmake -DOPENSSL_SSL_LIBRARIES=/usr/local/ssl/lib/libssl.so -DOPENSSL_CRYPTO_LIBRARIES=/usr/local/ssl/lib/libcrypto.so -DOPENSSL_INCLUDE_DIR=/usr/local/ssl/include ../ && make -j 16 && make install

RUN cp /root/TrinityCore/src/server/worldserver/worldserver.conf.dist /usr/local/etc/worldserver.conf
RUN cp /root/TrinityCore/src/server/bnetserver/bnetserver.conf.dist /usr/local/etc/bnetserver.conf

RUN mkdir /root/sql
RUN cp /root/TrinityCore/sql/base /root/sql/base -R
RUN cp /root/TrinityCore/sql/create /root/sql/create -R
RUN cp /root/TrinityCore/sql/custom /root/sql/custom -R
RUN cp /root/TrinityCore/sql/updates /root/sql/updates -R

RUN rm -rf /root/mysql-5.7.41
RUN rm -rf /root/openssl-1.0.2s
RUN rm -rf /root/TrinityCore

RUN mkdir /usr/local/logs
COPY extract /usr/local/bin/extract
COPY init /usr/local/bin/init
