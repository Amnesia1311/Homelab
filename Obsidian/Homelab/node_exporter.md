### Downlaod node_exporter

Download `node_exporter`
```bash
wget https://github.com/prometheus/node_exporter/releases/download/v1.4.0/node_exporter-1.4.0.linux-amd64.tar.gz
```

Entpacken `node_exporter
```bash
tar xzvf node_exporter-1.4.0.darwin-amd64
```

### Installation
node_exporter in das Verzeichnis kopieren:
```bash
mv node_exporter /usr/local/bin
```
User anlegen für node_exporter ohne login
```bash
useradd --no-create-home --shell /bin/false node_exporter
```
Rechte kontext auf User node_exporter ändern
```bash
chown node_exporter:node_exporter /usr/local/bin/node_exporter
```
#### Systemd Service erstellen

```bash
nano /etc/systemd/system/node_exporter.service

[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target

```

```bash
systemctl daemon-reload
systemctl start node_exporter
```