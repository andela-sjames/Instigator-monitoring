# Instigator-monitoring
Setup Monitoring for Instigator (Prometheus, Graphana and Kafka Exporter and JMX Kakfa Exporter)

You need to reference the [Instigator](https://github.com/andela-sjames/Instigator-monitoring) repo before running the docker-compose file on the repo. 


The Repo uses docker to set up monitoring for the I[Instigator](https://github.com/andela-sjames/Instigator-monitoring) Project Repository.

It has three main services

1. Kafka Exporter
2. Prometheus
3. Grafana


## Work Flow

Kafka exporter gets and pulls metrics from the kafka cluster, while prometheus stores these metrics in a time series DB database for Grafana to pull and display using really cool dashboads :)
