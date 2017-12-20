
FROM 172.30.254.171:5000/alm-registry/developer-hub-openjdk:2.0.5-SNAPSHOT

MAINTAINER Hygieia@capitalone.com

RUN \
  mkdir /hygieia

COPY *.jar /hygieia/
COPY sonar-codequality-properties-builder.sh /hygieia/

WORKDIR /hygieia

VOLUME ["/hygieia/logs"]

CMD ./sonar-codequality-properties-builder.sh && \
  java -jar sonar-codequality-collector*.jar --spring.config.location=/hygieia/hygieia-sonar-codequality-collector.properties

