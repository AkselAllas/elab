# Lab1 - Elastic cluster
Make sure you are in lab1 directory and following folders are present:
- esdata0
- esdata1
- esdata2

Bring up all containers:
```bash
$ docker-compose up
```
Show different cluster aspects:
```
curl -X GET -H 'Content-Type: application/json' http://localhost:9200/_cat/health
curl -X GET -H 'Content-Type: application/json' http://localhost:9200/_cat/nodes
curl -X GET -H 'Content-Type: application/json' http://localhost:9200/_cat/indices
curl -X GET -H 'Content-Type: application/json' http://localhost:9200/_cat/shards
```
Temporarily disable shard allocation:
```code
curl -X PUT -H 'Content-Type: application/json' http://localhost:9200/_cluster/settings -d \
'{
  "transient": {
    "cluster.routing.allocation.enable": "none"
  }
}'
```
Shut down first node and check cluster status
```bash
$ docker stop elasticsearch1
```
Shut down second node and check cluster status

Start first node again
```bash
$ docker start elasticsearch1
```
Enable shard allocation and check cluster status:
```code
curl -X PUT -H 'Content-Type: application/json' http://localhost:9200/_cluster/settings -d \
'{
  "transient": {
    "cluster.routing.allocation.enable": "all"
  }
}'
```
Start last node

Shut down all containers:
```bash
$ docker-compose down
```
