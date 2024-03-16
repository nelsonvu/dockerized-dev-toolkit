ARG DEBEZIUM_VERSION
FROM quay.io/debezium/connect:$DEBEZIUM_VERSION
ENV KAFKA_CONNECT_JDBC_DIR=$KAFKA_CONNECT_PLUGINS_DIR/kafka-connect-jdbc

ARG POSTGRES_VERSION=42.5.1
ARG KAFKA_JDBC_VERSION=5.3.2

# These should point to the driver version to be used
# ENV MAVEN_DEP_DESTINATION=$KAFKA_HOME/libs \
#     ORACLE_JDBC_REPO="com/oracle/database/jdbc" \
#     ORACLE_JDBC_GROUP="ojdbc8" \
#     ORACLE_JDBC_VERSION="19.22.0.0" \
#     ORACLE_JDBC_MD5=be9da9ba7f8b32d19ba2140de96a23e002aad1d4

# RUN docker-maven-download central "$ORACLE_JDBC_REPO" "$ORACLE_JDBC_GROUP" "$ORACLE_JDBC_VERSION" "$ORACLE_JDBC_MD5"

# Deploy Oracle JDBC Driver
COPY ojdbc8.jar $KAFKA_HOME/libs/ojdbc8.jar

# Deploy PostgreSQL JDBC Driver
RUN cd /kafka/libs && curl -sO https://jdbc.postgresql.org/download/postgresql-$POSTGRES_VERSION.jar

# Deploy Kafka Connect JDBC
RUN mkdir $KAFKA_CONNECT_JDBC_DIR && cd $KAFKA_CONNECT_JDBC_DIR &&\
	curl -sO https://packages.confluent.io/maven/io/confluent/kafka-connect-jdbc/$KAFKA_JDBC_VERSION/kafka-connect-jdbc-$KAFKA_JDBC_VERSION.jar

USER kafka
