# Monitoring
# Installation
The location for Grafana must be created before, so that the start of the container works. I assume here that you take the default user of the Linux (User ID 1000):
````bash
mkdir /var/docker/data/monitoring/grafana
chown 1000:1000 /var/docker/data/monitoring/grafana
````

## Grafana Datenquelle einrichten
After starting all containers, open the Grafana web interface and log in with ````admin/admin````.  
Then add a new "data source". The name can be freely assigned. Use ````http://mon_prometheus:9090```` as URL. Now click on "Save & Test" at the bottom. You should get a green field with the confirmation of the successful connection.
