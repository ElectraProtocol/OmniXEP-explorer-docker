FROM ubuntu:18.04
LABEL maintainer="TFinch <nexusnow@protonmail.com>"

#Install deps
RUN apt-get update
RUN apt-get install -y git-core \
                      pkg-config build-essential \
                      pyqt4-dev-tools python-qt4 python-dev python-twisted python-pip python-psutil \
                      swig \
                      libqtcore4 libqt4-dev libtool libpq-dev libffi-dev libssl-dev \
                      autotools-dev autoconf lsb-core supervisor wget \
                      build-essential libevent-dev libtool autotools-dev automake pkg-config \
                      bsdmainutils curl git libboost-all-dev libssl-dev libboost-tools-dev libdb++-dev \
                      libevent-dev libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools \
                      libprotobuf-dev protobuf-compiler libevent-dev libboost-all-dev libdb++-dev libssl-dev \
                      libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-program-options-dev \
                      libboost-test-dev libboost-thread-dev g++-arm-linux-gnueabihf gcc-aarch64-linux-gnu nsis libgmp3-dev \
                      libdb-dev zip unzip nano

ENV DATA_DIR=/root/.omnixep
ENV RPCALLOWIP="::/0"
ENV RPCUSER=omnicore
ENV RPCPASSWORD=omnicore

# Move the daemon and cli to a new folder outside of the source to better keep files clean
WORKDIR /root/

# Create the config file for omnixep and apply bootstrap for syncing
RUN mkdir /root/.omnixep/
WORKDIR /root/.omnixep/
RUN wget https://github.com/Jenova7/dev_bins/releases/download/dev_temp/omnixep.zip
RUN unzip omnixep.zip
RUN rm -rf omnixep.zip
#COPY omnixep.conf /root/.omnixep/

# Now make a new folder for the daemon and cli
WORKDIR /home/ubuntu/
RUN mkdir /home/ubuntu/core/
WORKDIR /home/ubuntu/core/

RUN wget https://github.com/MotoAcidic/omnilayer-explorer-docker/releases/download/1.0.1/omnixepd
RUN wget https://github.com/MotoAcidic/omnilayer-explorer-docker/releases/download/1.0.1/omnixep-cli
RUN chmod -R 755 omnixepd omnixep-cli
#RUN ./omnixepd -daemon

EXPOSE 8332-8333/tcp 16817-16818/tcp
VOLUME ["${DATA_DIR}"]

#ADD entrypoint.sh /entrypoint.sh

#RUN chmod u+x /entrypoint.sh

#ENTRYPOINT ["/entrypoint.sh"]
CMD ["./omnixepd"]