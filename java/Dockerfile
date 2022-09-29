FROM ubuntu:20.04

ARG DRIVER_VERSION=4.7.1
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y sudo \
    nano \
    gnupg \
    wget \
    default-jdk \
    maven \
    git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add - 
RUN echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.com/apt/ubuntu focal/mongodb-enterprise/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-enterprise.list
RUN apt-get update && apt-get install -y mongodb-enterprise mongodb-enterprise-cryptd

RUN export uid=1000 gid=1000 && \
    mkdir -p /home/ubuntu && \
    echo "ubuntu:x:${uid}:${gid}:Developer,,,:/home/ubuntu:/bin/bash" >> /etc/passwd && \
    echo "ubuntu:x:${uid}:" >> /etc/group && \
    echo "ubuntu ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/ubuntu && \
    chmod 0440 /etc/sudoers.d/ubuntu && \
    chown ${uid}:${gid} -R /home/ubuntu

ENV HOME /home/ubuntu

RUN mkdir -p ${HOME}/csfle/src/main/java/com/csfle
COPY ./csfle/pom.xml ${HOME}/csfle/pom.xml
COPY ./csfle/src/main/java/com/csfle/Example.java ${HOME}/csfle/src/main/java/com/csfle/Example.java 

RUN sed -i "s/x.x.x/${DRIVER_VERSION}/g" ${HOME}/csfle/pom.xml && chown -R ubuntu ${HOME}/csfle && chmod -R 750 ${HOME}/csfle

WORKDIR ${HOME}/csfle
USER ubuntu

CMD ["/bin/bash"]
