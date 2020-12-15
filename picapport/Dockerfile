FROM ubuntu
LABEL maintainer="pat@247.ch"

ARG VERSION=9-0-01

RUN apt-get update && \
    apt-get install -y default-jdk-headless

RUN mkdir -p /opt/picapport && mkdir -p /data/Pictures
ADD https://www.picapport.de/download/${VERSION}/picapport-headless.jar /opt/picapport/picapport-headless.jar

WORKDIR /opt/picapport

COPY picapport.properties /opt/picapport/.picapport/picapport.properties

RUN mkdir -p /opt/picapport/.picapport/groovy
ADD https://www.picapport.de/download/add-ons/pagpOSMGeoReverseEncoder-1.0.0.zip /opt/picapport/.picapport/groovy/pagpOSMGeoReverseEncoder-1.0.0.zip
ADD https://dl.bintray.com/groovy/maven/apache-groovy-binary-3.0.7.zip /opt/picapport/.picapport/groovy/apache-groovy-binary-3.0.7.zip

EXPOSE 8080
STOPSIGNAL SIGTERM

ENTRYPOINT ["java", "-XX:MaxMetaspaceSize=64m", "-Xms64m", "-Xmx1g", "-Xss4m", "-Duser.home=/opt/picapport", "-DTRACE=INFO", "-jar", "/opt/picapport/picapport-headless.jar"]
