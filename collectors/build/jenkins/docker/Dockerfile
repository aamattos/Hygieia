
FROM docker.io/openjdk:8-jre

MAINTAINER Hygieia@capitalone.com

RUN \
  mkdir /hygieia

COPY *.jar /hygieia/
COPY jenkins-build-properties-builder.sh /hygieia/

WORKDIR /hygieia

VOLUME ["/hygieia/logs"]

#IMPORT CERTIFICATES

ENV JAVA_HOME=/docker-java-home/jre
ENV CUSTOM_KEYSTORE=/etc/ssl/certs
ARG CLUSTER_PUBLIC_HOSTNAME=devos.alm.totta.dev.corp


RUN $JAVA_HOME/bin/keytool -printcert -rfc -sslServer $CLUSTER_PUBLIC_HOSTNAME >>  $CUSTOM_KEYSTORE/alm-totta.pem && \
		$JAVA_HOME/bin/keytool -printcert -rfc -sslServer hipchat.ci.gsnet.corp >>  $CUSTOM_KEYSTORE/hipchat.pem && \
		$JAVA_HOME/bin/keytool -printcert -rfc -sslServer gitlab.alm.gsnetcloud.corp >>  $CUSTOM_KEYSTORE/gitlab.pem

RUN $JAVA_HOME/bin/keytool -storepasswd -new mysecretpassword -keystore $JAVA_HOME/lib/security/cacerts -storepass changeit && \
		echo "yes" | $JAVA_HOME/bin/keytool -import -trustcacerts -file $CUSTOM_KEYSTORE/alm-totta.pem -alias my-root-ca -keystore $JAVA_HOME/lib/security/cacerts -storepass mysecretpassword && \
		echo "yes" | $JAVA_HOME/bin/keytool -import -trustcacerts -file $CUSTOM_KEYSTORE/hipchat.pem -alias hipchat -keystore $JAVA_HOME/lib/security/cacerts -storepass mysecretpassword && \
		echo "yes" | $JAVA_HOME/bin/keytool -import -trustcacerts -file $CUSTOM_KEYSTORE/gitlab.pem -alias gitlab -keystore $JAVA_HOME/lib/security/cacerts -storepass mysecretpassword

#Fim instalado certificados

CMD ./jenkins-build-properties-builder.sh && \
  java -jar jenkins-build-collector*.jar --spring.config.location=/hygieia/hygieia-jenkins-build-collector.properties

