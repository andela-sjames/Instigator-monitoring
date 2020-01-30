# Instigator-monitoring

Setup Monitoring for Instigator (Prometheus, Graphana and Kafka Exporter and JMX Kakfa Exporter)

You need to reference the [Instigator](https://github.com/andela-sjames/Instigator-monitoring) repo before running the docker-compose file on the repo.

The Repo uses docker to set up monitoring for the I[Instigator](https://github.com/andela-sjames/Instigator-monitoring) Project Repository.

It has three main services

1. Kafka Exporter
2. Prometheus
3. Grafana

## Work Flow

Kafka exporter gets and pulls metrics from the kafka cluster, while prometheus stores these metrics in a time series database for Grafana to pull and display using really cool dashboads :)

Prometheus also keeps track of the services it's pull metrics from and one of such metric is the metric it pulls from each brokers within the kafka cluster called Kafka JMX metrics

```yaml
- job_name: 'kafka_jmx_exporter'
    static_configs:
    - targets:
      - instigator_broker_1:7072
      - instigator_broker_2:7072
      - instigator_broker_3:7072

```

The kafka brokers from the Instigator repository have the prometheus java agent and jmx exporter installed in them. Reference the kafka Dockerfile.

So what's the difference between the Kafka Exporter and the Kafka JMX Exporter? The former is cluster specific while the later is node specific metric!
