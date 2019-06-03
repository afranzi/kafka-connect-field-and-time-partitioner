# Kafka Connect Field and Time Based Partitioner

- Partition initially by a custom field and then by time.
- It extends **[TimeBasedPartitioner](https://github.com/confluentinc/kafka-connect-storage-common/blob/master/partitioner/src/main/java/io/confluent/connect/storage/partitioner/TimeBasedPartitioner.java)**, so any existing time based partition config should be fine.

## Required properties

- `partitioner.class=com.canelmas.kafka.connect.FieldAndTimeBasedPartitioner`
- `partition.field=<custom field in your record>`
- `partition.name=<partition_name>`

## Config Example

```
partition.field=data.type
partition.name=sensor
path.format='year='YYYY/'month='MM/'day='dd/'hour='HH
topics.dir=garden/sensors
s3.bucket.name=our_s3_bucket
```

This configuration will produce the following output:

- `s3://our_s3_bucket/garden/sensors/sensor=lux/year=2019/month=06/day=12/part-xxxx.json`
- `s3://our_s3_bucket/garden/sensors/sensor=soil_moisture/year=2019/month=06/day=12/part-xxxx.json`
- `s3://our_s3_bucket/garden/sensors/sensor=sound/year=2019/month=06/day=12/part-xxxx.json`
- `s3://our_s3_bucket/garden/sensors/sensor=temperature/year=2019/month=06/day=12/part-xxxx.json`
