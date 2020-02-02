# Instigator-monitoring

Setup Monitoring for Instigator (Prometheus, Graphana, Kafka Exporter and JMX Kakfa Exporter)

**Please Note** that this setup will not run if the Instigator project is not started first.

You need to reference the [Instigator](https://github.com/andela-sjames/Instigator-monitoring) repo before running the docker-compose file on the repo.

This Repo uses docker to set up monitoring for the [Instigator](https://github.com/andela-sjames/Instigator-monitoring) Project Repository.

It has three main services:

1. [Kafka Exporter](https://github.com/danielqsj/kafka_exporter)
2. [Prometheus](https://prometheus.io/docs/introduction/overview/)
3. [Grafana](https://grafana.com/)

[Grafana support for prometheus](https://prometheus.io/docs/visualization/grafana/)

## Work Flow

Kafka exporter gets and pulls metrics from the kafka cluster, while prometheus stores these metrics in a time series database for Grafana to pull and display on cool dashboads :)

Prometheus also keeps track of the services it's pull metrics from and one of such metric is the metric it pulls from each brokers within the kafka cluster called Kafka JMX metrics

```yaml
# prometheus.yml file

- job_name: 'kafka_jmx_exporter'
    static_configs:
    - targets:
      - instigator_broker_1:7072
      - instigator_broker_2:7072
      - instigator_broker_3:7072

```

The kafka brokers from the Instigator repository have the `prometheus java agent` and `jmx exporter` installed on them. Please reference the kafka Dockerfile.

So what's the difference between the `Kafka Exporter` and the `Kafka JMX Exporter`? The former is a cluster specific metric while the later is a node specific metric!

## Network

The Docker-Compose file uses an already existing network when running locally called `Instigator`

```yaml

networks:
  Instigator:
      external: true
```

This network is created when you start the Instigator project. **Please note** that this setup will not run if the Instigator project is not started first.

## Network Inspection

To see how docker allows services to talk to each other within a network, you should inspect docker network settings via the command

```shell
$docker network inspect Instigator
```

This will show you the IP addresses and the service names Docker assigns to every running container within the network once it is running.

## Running Docker

```shell
$docker-compose up
```

This will build and start all containers if called the first time, every other time the command is called will run the stack without builing.

## Accessing the Services

### Kafka Exporter

```shell
localhost:9308
```

### Prometheus

```shell
localhost:9090
```

### Grafana

```shell
user: admin
password: pass
```

```shell
localhost:3000
```

## What's Next

Learn about these tools:

- <https://prometheus.io/docs/prometheus/latest/getting_started/>
- <https://www.robustperception.io/monitoring-kafka-with-prometheus>
- <https://grafana.com/docs/grafana/latest/tutorials/>
