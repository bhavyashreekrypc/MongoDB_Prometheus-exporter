
# MongoDB Monitoring with Grafana & Prometheus
Prometheus scrapes targets. Targets may be instrumented applications (like instrumented Java apps for example), the Pushgateway, or exporters.


Exporters are a way to bind to an existing entity (a database, a reverse proxy server, an application server) to expose metrics to Prometheus.

The MongoDB exporter is one of them.

Prometheus will bind to the MongoDB exporters and store related metrics in its own internal storage system.

From there, Grafana will bind to Prometheus and display metrics on dashboard panels.


## Documentation
Referance:

[Documentation1](https://www.junosnotes.com/guide/mongodb-monitoring-with-grafana-prometheus/)

[Documentation2](https://www.digitalocean.com/community/tutorials/how-to-monitor-mongodb-with-grafana-and-prometheus-on-ubuntu-20-04)

[docker-compose](https://github.com/bhavyashreekrypc/MongoDB_Prometheus-exporter/blob/main/docker-compose.yaml)

[prometheus.yml](https://github.com/bhavyashreekrypc/MongoDB_Prometheus-exporter/blob/main/prometheus.yml)

[issues](https://github.com/percona/mongodb_exporter/issues/621)




## Installation

Install all the required services with docker



## Steps:
1. docker-compose up -d
2. sudo chmod 777 grafana-etc/ grafana-lib/ grafana-log/ grafana.ini prometheus.yml
3. then do compose down and up -d
4. URLs
http://localhost:9090 -prometheus

http://localhost:9216 -mongodb_exporter

http://localhost:3001 -grafana

5. So once the services are up you will set up MongoDB authentication for the MongoDB exporter and create a user to monitor the cluster’s metrics
```bash
docker exec -it mongodb_mongodb_1 mongosh -u root -p root
> use admin
> db.createUser( { user: "exporter", pwd: "password", roles: [ { role: "clusterMonitor", db: "admin" }, { role: "read", db: "local" }] })

output: screenshot1
```
6. export MONGODB_URI=mongodb://exporter:password@localhost:27017
7. sudo curl http://localhost:9216/metrics


   
    
## Troubleshooting
error1:           
"panel plugin not found: grafana-polystat-panel error"

[download grafaa-polystat]](https://grafana.com/api/plugins/grafana-polystat-panel/versions/2.0.9/download)
```
wget https://grafana.com/api/plugins/grafana-polystat-panel/versions/2.0.9/download
unzip grafana-polystat-panel-2.0.9.zip
mv grafana-polystat-panel ~/grafana-lib/plugins
docker-compose up -d
```
