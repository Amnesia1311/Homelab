### Download & Installation go
Download von go
```bash
wget https://go.dev/dl/go1.19.2.linux-amd64.tar.gz
tar xzvf go1.19.2.linux-amd64.tar.gz
```

Installation go:
```bash
cd go
mv go /usr/local/
export PATH=$PATH:/usr/local/go/bin
```
### Installation 3cx_exporter
Klonen git repo
```bash
git clone https://github.com/digineo/3cx_exporter.git
```
Installation 3cx_exporter
```bash
cd 3cx_exporter/
nano config.json
go build
mv 3cx_exporter /usr/bin/
mkdir -p  /etc/3cx_exporter/
cp fixtures/config.json /etc/3cx_exporter/
```

Systemd service für 3cx_exporter erstellen:
```bash
nano /etc/systemd/system/3cx_exporter.service

[Unit]
Description=3CX Prometheus Exporter
After=network.target

[Service]
Type=simple
Restart=always
ExecStart=/usr/bin/3cx_exporter -config /etc/3cx_exporter/config.json
```

#### Firewall regeln 
3cx verwendet (**nftables**)[[nftables]]. Somit muss der Port erst freigegeben werden, sodass von außen auf diesen zugegriffen werden kann.
```bash
tcp dport 9523 ip saddr 192.168.178.0/24 accept;
```
