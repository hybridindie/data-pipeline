FROM python:3.10-slim as base

# Setup env
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONFAULTHANDLER 1
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk-amd64/

RUN apt update && apt install -y --no-install-recommends \
    gcc g++ python3-dev libpq-dev libxml2 curl procps \
    libxslt-dev nodejs npm openjdk-11-jre-headless


FROM base AS runtime

ARG SPARK_VERSION=3.2.1
ARG HADOOP_VERSION=3.2

RUN curl https://archive.apache.org/dist/spark/spark-$SPARK_VERSION/spark-$SPARK_VERSION-bin-hadoop$HADOOP_VERSION.tgz -o spark.tgz && \
    tar -xf spark.tgz && \
    mv spark-$SPARK_VERSION-bin-hadoop$HADOOP_VERSION /opt/spark && \
    mkdir -p /opt/spark/logs && \
    rm spark.tgz

ENV PYSPARK_PYTHON python3

WORKDIR /opt/workspace