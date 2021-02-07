FROM gcr.io/google-containers/zeppelin:v0.5.6_v1
LABEL maintainer="kumar.vivek2696@gmail.com"

RUN sed -i '/jessie-updates/d' /etc/apt/sources.list
RUN echo "deb [check-valid-until=no] http://cdn-fastly.deb.debian.org/debian jessie main" > /etc/apt/sources.list.d/jessie.list
RUN echo "deb [check-valid-until=no] http://archive.debian.org/debian jessie-backports main" > /etc/apt/sources.list.d/jessie-backports.list
RUN sed -i '/deb http:\/\/deb.debian.org\/debian jessie-updates main/d' /etc/apt/sources.list
RUN apt-get -o Acquire::Check-Valid-Until=false update

RUN apt-key adv --recv-keys --keyserver keyserver.ubuntu.com AA8E81B4331F7F50

RUN apt-get -y -o Acquire::Check-Valid-Until=false  update && \
    apt-get -y upgrade && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Credits: @jeffharwell https://github.com/jeffharwell/zeppelin/blob/master/Dockerfile
RUN wget https://downloads.apache.org/zeppelin/zeppelin-0.8.2/zeppelin-0.8.2-bin-all.tgz && \
    tar -xvf ./zeppelin-0.8.2-bin-all.tgz && \
    mkdir /config_backup && \
    cp /opt/zeppelin/conf/* /config_backup && \
    mkdir /run_backup && \
    cp /opt/zeppelin/bin/* /run_backup && \
    rm -fr /opt/zeppelin && \
    mv ./zeppelin-0.8.2-bin-all /opt/zeppelin && \
    ls /config_backup/ && \
    cp /config_backup/zeppelin-env.sh /opt/zeppelin/conf/ && \
    cp /config_backup/log4j.properties /opt/zeppelin/conf/ && \
    cp /run_backup/docker-zeppelin.sh /opt/zeppelin/bin/ && \
    rm -fr /config_backup && \
    rm -fr /run_backup && \
    rm ./zeppelin-0.8.2-bin-all.tgz && \
    rm -rf /tmp/* /var/tmp/*

RUN wget https://archive.apache.org/dist/spark/spark-2.3.2/spark-2.3.2-bin-hadoop2.7.tgz && \
    tar -xvf ./spark-2.3.2-bin-hadoop2.7.tgz && \
    mkdir /config_backup && \
    cp /opt/spark/conf/* /config_backup && \
    cp /opt/spark/lib/gcs-connector-latest-hadoop2.jar /config_backup && \
    rm -fr /opt/spark-1.5.2-bin-hadoop2.6 && \
    rm /opt/spark && \
    mv ./spark-2.3.2-bin-hadoop2.7 /opt/ && \
    ln -s /opt/spark-2.3.2-bin-hadoop2.7 /opt/spark && \
    cp /config_backup/core-site.xml /opt/spark/conf && \
    cp /config_backup/log4j.properties /opt/spark/conf && \
    cp /config_backup/spark-defaults.conf /opt/spark/conf && \
    cp /config_backup/gcs-connector-latest-hadoop2.jar /opt/spark/lib && \
    rm -fr /config_backup && \
    rm ./spark-2.3.2-bin-hadoop2.7.tgz