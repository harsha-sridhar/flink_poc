# Using Flink Kafka Connector and Kafka S3 connector

## Run Postgres and grafana
```shell
cd docker/postgres+grafana
docker-compose up
```

## Setup Flink (Ignore if already done)
Follow the steps [here](Flink_setup.md)

## Start Flink
```shell
start-cluster.sh
```

## Setup Kafka (Ignore if already done)
Follow the steps [here](Kafka_setup.md)

## Download Kafka Connector
```shell
confluent-hub install confluentinc/kafka-connect-s3-source:latest
```

## Start confluent kafka and related components (If not already running)
```shell
confluent local services start
```

## Start the connector
```shell
confluent local services connect connector load quick-start-s3-source -c s3_connector.json
```

## Check the status of the connector
```shell
$ confluent local services connect connector status quick-start-s3-source

The local commands are intended for a single-node development environment only,
NOT for production usage. https://docs.confluent.io/current/cli/index.html

{
  "name": "quick-start-s3-source",
  "connector": {
    "state": "RUNNING",
    "worker_id": "127.0.1.1:8083"
  },
  "tasks": [
    {
      "id": 0,
      "state": "RUNNING",
      "worker_id": "127.0.1.1:8083"
    }
  ],
  "type": "source"
}
```

## Submit Flink job
```shell
sql-client.sh -i flink_sql/initialization_scripts/channel_stats_init.sql -f flink_sql/queries/channel_stats.sql
```

## Issues with s3_connector
The connector won’t reload data during the following scenarios:
> Renaming a file which the connector has already read. <br/>
> Uploading a newer version of a file with a new record.