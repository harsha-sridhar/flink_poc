# Flink POC

## Repo Structure
    docker
        - postgres+grafana -> contains all
    docs
        All documentation
    flink_sql
        - initialization_scripts (contains the initialization scripts for flink sql job)
        - queries (contains the query files that should be run post initialization)
    kafka
        consists of connector files
    kubernetes
        consists of helm charts required to setup HA flink cluster

## Local setup
    Follow the docs - [Flink Setup](Flink_setup.md), [Kafka Setup](Kafka_setup.md) and [Job Setup](flink_kafka.md) in the same order
