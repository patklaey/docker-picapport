FROM ubuntu
LABEL maintainer="pat@247.ch"

ARG VERSION=8-2-02

RUN apt-get update && \
    apt-get install -y default-jdk-headless

RUN mkdir -p /opt/picapport && mkdir -p /data/Pictures
ADD https://www.picapport.de/download/${VERSION}/picapport-headless.jar /opt/picapport/picapport-headless.jar

WORKDIR /opt/picapport

COPY picapport.properties /opt/picapport/.picapport/picapport.properties

EXPOSE 8080
STOPSIGNAL SIGTERM

ENTRYPOINT ["java", "-XX:MaxMetaspaceSize=64m", "-Xms64m", "-Xmx512m", "-Xss4m", "-Duser.home=/opt/picapport", "-DTRACE=INFO", "-jar", "/opt/picapport/picapport-headless.jar"]
