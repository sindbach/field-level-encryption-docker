FROM ubuntu:20.04

ARG DRIVER_VERSION=3.6.2
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y sudo \
    nano \
    gnupg \
    git \
    nodejs \
    wget \
    npm \
    build-essential && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | apt-key add -

RUN echo "deb [ arch=amd64,arm64,s390x ] http://repo.mongodb.com/apt/ubuntu focal/mongodb-enterprise/4.4 multiverse" | tee /etc/apt/sources.list.d/mongodb-enterprise.list

RUN apt-get update && apt-get install -y mongodb-enterprise-cryptd=4.4.1

RUN export uid=1000 gid=1000 && \
    mkdir -p /home/ubuntu && \
    echo "ubuntu:x:${uid}:${gid}:Developer,,,:/home/ubuntu:/bin/bash" >> /etc/passwd && \
    echo "ubuntu:x:${uid}:" >> /etc/group && \
    echo "ubuntu ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/ubuntu && \
    chmod 0440 /etc/sudoers.d/ubuntu && \
    chown ${uid}:${gid} -R /home/ubuntu

ENV HOME /home/ubuntu

USER ubuntu

RUN mkdir ${HOME}/csfle
COPY ./csfle/example.js ./csfle/package.json ${HOME}/csfle/

WORKDIR ${HOME}/csfle
RUN npm install mongodb@${DRIVER_VERSION} mongodb-client-encryption uuid-mongodb --save

CMD ["/bin/bash"]
