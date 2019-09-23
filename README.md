# Apache Livy Docker Container

Based on the latest release of the [Apache Livy project](https://livy.incubator.apache.org/)


YARN version


docker build -t livy-server-docker:yarn .

docker run -d --net=host -p 8998:8998 -h ecsa00400b48.epam.com \
-e SPARK_KAFKA_VERSION=0.10 \
-e HADOOP_CONF_DIR=/etc/hadoop/conf \
-v /opt/cloudera/parcels/SPARK2/lib/spark2:/opt/spark2 \
-v /opt/cloudera/parcels:/opt/cloudera/parcels \
-v /etc/hadoop/conf:/etc/hadoop/conf \
-v /tmp:/tmp livy-server-docker:yarn

curl -X POST --data {kind: spark} -H "Content-Type: application/json" ecsa00400b48.epam.com:8998/sessions

curl ecsa00400b48.epam.com:8998/sessions/0/statements -X POST -H 'Content-Type: application/json' -d '{code:val rdd = sc.parallelize(Array(1,2,3,4,5,6,7,8,9,10))}'

curl ecsa00400b48.epam.com:8998/sessions/0/statements -X POST -H 'Content-Type: application/json' -d '{code:rdd.collect().foreach(println)}'


export HADOOP_JARS=/opt/cloudera/parcels/CDH/jars
export HADOOP_CLASSPATH=$(find $HADOOP_JARS -name '*.jar' | xargs echo | tr ' ' ':')

#!/usr/bin/env bash

export SPARK_HOME=/opt/cloudera/parcels/SPARK2/lib/spark2
export HADOOP_CONF_DIR=/etc/hadoop/conf
export JAVA_HOME=/usr/java/jdk1.8.0_144
export SPARK_KAFKA_VERSION=0.10

./bin/livy-server start


curl -X POST --data @Z_RECORDS_resend.json -H "Content-Type: application/json" ecsa00400b48.epam.com:8998/batches
