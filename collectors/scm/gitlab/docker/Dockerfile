
FROM 172.30.254.171:5000/alm-registry/developer-hub-openjdk:2.0.5-SNAPSHOT

MAINTAINER Hygieia@capitalone.com

RUN \
  mkdir /hygieia

COPY *.jar /hygieia/
COPY gitlab-properties-builder.sh /hygieia/

WORKDIR /hygieia

VOLUME ["/hygieia/logs"]

CMD ./gitlab-properties-builder.sh && \
  java -jar gitlab-scm-collector*.jar --spring.config.location=/hygieia/hygieia-gitlab-scm-collector.properties

