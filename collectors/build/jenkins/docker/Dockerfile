
FROM 172.30.254.171:5000/alm-registry/developer-hub-openjdk:2.0.5-SNAPSHOT

MAINTAINER Hygieia@capitalone.com

RUN \
  mkdir /hygieia

COPY *.jar /hygieia/
COPY jenkins-build-properties-builder.sh /hygieia/

WORKDIR /hygieia

VOLUME ["/hygieia/logs"]

CMD ./jenkins-build-properties-builder.sh && \
  java -jar jenkins-build-collector*.jar --spring.config.location=/hygieia/hygieia-jenkins-build-collector.properties

