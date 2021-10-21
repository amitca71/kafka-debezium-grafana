ARG DEBEZIUM_VERSION
FROM debezium/connect:${DEBEZIUM_VERSION}
ENV KAFKA_CONNECT_JDBC_DIR=$KAFKA_CONNECT_PLUGINS_DIR/kafka-connect-jdbc \
    KAFKA_CONNECT_S3_DIR=$KAFKA_CONNECT_PLUGINS_DIR/kafka-connect-s3

ARG POSTGRES_VERSION=42.2.8
ARG KAFKA_JDBC_VERSION=5.3.2
ARG KAFKA_S3_VERSION=10.0.2


# Deploy PostgreSQL JDBC Driver
RUN cd /kafka/libs && curl -sO https://jdbc.postgresql.org/download/postgresql-$POSTGRES_VERSION.jar

# Deploy Kafka Connect JDBC
RUN mkdir $KAFKA_CONNECT_JDBC_DIR && cd $KAFKA_CONNECT_JDBC_DIR &&\
	curl -sO https://packages.confluent.io/maven/io/confluent/kafka-connect-jdbc/$KAFKA_JDBC_VERSION/kafka-connect-jdbc-$KAFKA_JDBC_VERSION.jar

# Deploy Kafka Connect S3
RUN mkdir $KAFKA_CONNECT_S3_DIR && cd $KAFKA_CONNECT_S3_DIR
 COPY confluentinc-kafka-connect-s3-10.0.0/ $KAFKA_CONNECT_S3_DIR/
#	curl -sO https://packages.confluent.io/maven/io/confluent/kafka-connect-s3/$KAFKA_S3_VERSION/kafka-connect-s3-$KAFKA_S3_VERSION.jar

ARG JMX_AGENT_VERSION
 RUN mkdir /kafka/etc && cd /kafka/etc &&\
         curl -so jmx_prometheus_javaagent.jar \
         https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/$JMX_AGENT_VERSION/jmx_prometheus_javaagent-$JMX_AGENT_VERSION.jar
 
 COPY config.yml /kafka/etc/config.yml
