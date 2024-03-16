FROM confluentinc/cp-kafka-connect:7.4.1

LABEL maintainer="NelsonVu"

USER root
RUN yum install unzip -y

COPY jars/*.jar /etc/kafka-connect/jars

# confluentinc-kafka-connect-jdbc
ADD confluentinc-kafka-connect-jdbc-10.7.4.zip /tmp/confluentinc-kafka-connect-jdbc.zip
RUN unzip /tmp/confluentinc-kafka-connect-jdbc.zip -d /usr/share/java && rm /tmp/confluentinc-kafka-connect-jdbc.zip

# confluentinc-kafka-connect-oracle
ADD confluentinc-kafka-connect-oracle-cdc-2.11.1.zip /tmp/confluentinc-kafka-connect-oracle-cdc.zip
RUN unzip /tmp/confluentinc-kafka-connect-oracle-cdc.zip -d /usr/share/java && rm /tmp/confluentinc-kafka-connect-oracle-cdc.zip

# confluentinc-kafka-connect-oracle
ADD OGG_BigData_Linux_x64_19.1.0.0.5.zip /tmp/OGG_BigData_Linux_x64.zip
RUN unzip /tmp/OGG_BigData_Linux_x64.zip -d /usr/share/java && rm /tmp/OGG_BigData_Linux_x64.zip
