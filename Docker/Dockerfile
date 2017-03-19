# This is a comment
FROM maven:3.3
MAINTAINER PhilippGrulich
RUN apt-get update
RUN apt-get -y install git
RUN apt-get -y install curl
RUN apt-get -y install libfontconfig
# Install nodejs
RUN curl -sL https://deb.nodesource.com/setup_6.x -o i.sh
RUN bash i.sh
Run apt-get install -y nodejs
RUN apt-get install -y build-essential

# install rabbitmq

RUN echo 'deb http://www.rabbitmq.com/debian/ testing main' | tee /etc/apt/sources.list.d/rabbitmq.list && wget -O- https://www.rabbitmq.com/rabbitmq-release-signing-key.asc | apt-key add - && apt-get update && apt-get install -y rabbitmq-server && invoke-rc.d rabbitmq-server start &&  rabbitmq-plugins enable rabbitmq_management

# clone zeppelin

RUN git clone https://github.com/TU-Berlin-DIMA/zeppelin.git && cd zeppelin && git checkout i2-zeppelin 

RUN cd zeppelin  && mvn clean package -DskipTests 

WORKDIR zeppelin/
EXPOSE 8080 15672 8081
CMD bin/zeppelin-daemon.sh start && rabbitmq-server && tail -f /dev/null
