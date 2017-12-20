
FROM 172.30.254.171:5000/alm-registry/developer-hub-openjdk:2.0.5-SNAPSHOT

MAINTAINER Hygieia@capitalone.com

RUN \

  mkdir  /hygieia

COPY *.jar /hygieia/
COPY jira-properties-builder.sh /hygieia/

WORKDIR /hygieia/

VOLUME ["/hygieia/logs"]

CMD ./jira-properties-builder.sh &&\
	 java -jar jira-feature-collector*.jar --debug --spring.config.location=hygieia-jira-feature-collector.properties
