ARG DEBEZIUM_VERSION
FROM quay.io/debezium/connect:$DEBEZIUM_VERSION

ENV KAFKA_CONNECT_JDBC_DIR=$KAFKA_CONNECT_PLUGINS_DIR/kafka-connect-jdbc
ENV KAFKA_CONNECT_ES_DIR=$KAFKA_CONNECT_PLUGINS_DIR/kafka-connect-elasticsearch
ENV CONFLUENT_VERSION=7.0.1 \
    AVRO_VERSION=1.10.1 \
    GUAVA_VERSION=31.0.1-jre

ARG POSTGRES_VERSION=42.5.1
ARG KAFKA_JDBC_VERSION=5.3.2
ARG KAFKA_ELASTICSEARCH_VERSION=5.3.2

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

RUN docker-maven-download confluent kafka-connect-avro-converter "$CONFLUENT_VERSION" fd03a1436f29d39e1807e2fb6f8e415a && \
        docker-maven-download confluent kafka-connect-avro-data "$CONFLUENT_VERSION" d27f30e9eca4ef1129289c626e9ce1f1 && \
        docker-maven-download confluent kafka-avro-serializer "$CONFLUENT_VERSION" c72420603422ef54d61f493ca338187c && \
        docker-maven-download confluent kafka-schema-serializer "$CONFLUENT_VERSION" 9c510db58119ef66d692ae172d5b1204 && \
        docker-maven-download confluent kafka-schema-registry-client "$CONFLUENT_VERSION" 7449df1f5c9a51c3e82e776eb7814bf1 && \
        docker-maven-download confluent common-config "$CONFLUENT_VERSION" aab5670de446af5b6f10710e2eb86894 && \
        docker-maven-download confluent common-utils "$CONFLUENT_VERSION" 74bf5cc6de2748148f5770bccd83a37c && \
        docker-maven-download central org/apache/avro avro "$AVRO_VERSION" 35469fee6d74ecbadce4773bfe3a204c && \
        docker-maven-download central com/google/guava guava "$GUAVA_VERSION" bb811ca86cba6506cca5d415cd5559a7

# --- MongoDB CDC Connector (Debezium 3.0) ---
# We download the full plugin archive to ensure all driver dependencies are included
ENV KAFKA_CONNECT_MONGODB_DIR=$KAFKA_CONNECT_PLUGINS_DIR/debezium-connector-mongodb

RUN cd $KAFKA_CONNECT_MONGODB_DIR && \
    curl -sO https://repo1.maven.org/maven2/io/debezium/debezium-connector-mongodb/3.0.0.Final/debezium-connector-mongodb-3.0.0.Final-plugin.tar.gz && \
    tar -xzf debezium-connector-mongodb-3.0.0.Final-plugin.tar.gz --strip-components=1 && \
    rm debezium-connector-mongodb-3.0.0.Final-plugin.tar.gz

# --- Apache Iceberg Sink Connector ---
# Note: Iceberg 1.4.x+ is recommended for modern Kafka Connect setups
ENV KAFKA_CONNECT_ICEBERG_DIR=$KAFKA_CONNECT_PLUGINS_DIR/kafka-connect-iceberg
ARG ICEBERG_VERSION=0.6.17

RUN mkdir $KAFKA_CONNECT_ICEBERG_DIR && cd $KAFKA_CONNECT_ICEBERG_DIR && \
    curl -sO https://repo1.maven.org/maven2/io/tabular/iceberg-kafka-connect-runtime/$ICEBERG_VERSION/iceberg-kafka-connect-runtime-$ICEBERG_VERSION.jar

USER kafka
