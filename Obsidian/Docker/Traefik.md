# What is Traefik
Traefik is a reverse proxy that can automatically generate certificates via Lets encrypt.

## Prerequisite
- OS with Docker & Docker Compose installed
- Domain with DNS api support

### Goals
- Treafik rollout
- TLS activation
- Automatically generate wildcard Lets encrypt certificates

## Create Docker network

```bash
docker network create proxy
```

## ACME file
Traefik will store all information about the certificates in acme.json file.
```bash
cd data
chmod 600 acme.json
```


## Dashboard
If the Traefik Dashboard is to be used, a user + password must be created with `apache2-utils` as follows.
```bash
sudo apt install apache2-utils -y
```
 
```bash
echo $(htpasswd -nbB <USER> "<PASS>") | sed -e s/\\$/\\$\\$/g
```
Then copy the line and enter it in the .env file in the variable `DASHBOARD_USER´.
```bash
DASHBOARD_USER=XXX
```
Afterwards the dashboard can be used at https://traefik.example.com


 [YouTube Kanals](https://youtube.com/teqqyde)
[ssllabs](https://www.ssllabs.com/ssltest/).