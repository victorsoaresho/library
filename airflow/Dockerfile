FROM apache/airflow:2.9.0-python3.9

ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
ENV PATH="${JAVA_HOME}/bin:${PATH}"

USER root
RUN apt-get update && \
    apt-get install -y openjdk-11-jdk && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

USER airflow

RUN pip install --no-cache-dir pyspark==3.5.1 findspark

COPY ./dags /opt/airflow/dags

EXPOSE 8080

CMD airflow db init && \
    airflow scheduler & \
    airflow webserver
