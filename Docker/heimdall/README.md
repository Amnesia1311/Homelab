## Installation
The .env must be adapted accordingly at the beginning.
Start the container with `docker-compose up -d`.
If you want to password protect heimdall you can do this with the following command.
```bash
docker exec -it heimdall htpasswd -c /config/nginx/.htpasswd <EXAMPLE_USER>
```