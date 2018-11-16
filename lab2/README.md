Make sure you are in lab2 directory and following folders are present:
- esdata0
- lsdata/pipeline
- lsdata/input
Bring up all containers:
```bash
$ docker-compose up
```
Logstash default pipeline configuration is located in lsdata/pipeline folder.
Change Logstash to use Elasticsearch as an output:

``````
output {
  elasticsearch {
    hosts => ["http://elasticsearch0-lab2:9200"]
    index => "logstash-0"
  }
}
``````
Create index pattern in Kibana

Write something to the end of lsdata/input/messages0
```bash
echo "test2" >> lsdata/input/messages0
```
Start passing access log to Logstash input
```bash
while IFS= read -r line; do echo $line >> lsdata/input/messages0 ; sleep 1; done < ../NASA_access_log_Jul95
```
Create simple dissect filter to parse log

``````
filter {
  dissect {
    mapping => {
      "message" => "%{aadress} - - [%{aeg} %{sisu}"
    }
  }
}
``````
Add geoip processing:
``````
geoip {
  source =>"aadress"
}
``````
Add timestamp processing:
``````
date {
  match => ["aeg", "dd/MMM/yyyy:HH:mm:ss Z"]
}
``````
Process logs conditionally:
``````
if ("_geoip_lookup_failure" in [tags]) {
  mutate {
    add_field => {"foo" => "geoip_jama"}
  }
}
``````
Move to use predefined patterns:
``````
grok {
  match => { "message" => "%{COMMONAPACHELOG}"}
}
``````
