# Installation
The .env must be adapted to your own requirements.
After that the service can be started with `docker-compose up -d`.
As soon as the container is up, perform the installation steps on the NextCloud website.

Without these steps the nextcloud frontend is very slow for me.
1. `docker inspect traefik`
2. Change config file `/var/docker/nextcloud/app/config/config.php`
```bash
'trusted_proxies' => '172.18.0.3/16'
'overwrite.cli.url' => 'https://nextcloud.example.com',
'overwriteprotocol' => 'https',
'overwritehost' => 'nextcloud.example.com',
```
3. DB Optimierung 
```bash
docker exec --user www-data nextcloud-app php occ db:add-missing-indices
docker exec --user www-data nextcloud-app php occ db:convert-filecache-bigint
```
4. Container neu starten:
```bash
docker-compose stop
docker-compose rm -f
docker-compose up -d
```
