# Apache Livy Docker Container

Based on the latest release of the [Apache Livy project](https://livy.incubator.apache.org/)


YARN version

docker build -t livy-server-docker:yarn .

docker run -d --net=host -p 8998:8998 -h ecsa00400b48.epam.com -e SPARK_KAFKA_VERSION=0.10 -e HADOOP_CONF_DIR=/etc/hadoop/conf -v /etc/hadoop/conf:/etc/hadoop/conf -v /tmp:/tmp livy-server-docker:yarn



curl -X POST --data {kind: spark} -H "Content-Type: application/json" ecsa00400b48.epam.com:8998/sessions

curl ecsa00400b48.epam.com:8998/sessions/0/statements -X POST -H 'Content-Type: application/json' -d '{code:val rdd = sc.parallelize(Array(1,2,3,4,5,6,7,8,9,10))}'

curl ecsa00400b48.epam.com:8998/sessions/0/statements -X POST -H 'Content-Type: application/json' -d '{code:rdd.collect().foreach(println)}'
