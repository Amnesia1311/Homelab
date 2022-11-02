# Installation
Adjust the URL in the env file accordingly
After this start the container with `docker-compose up -d`.

Then go to the website and log in. Afterwards complete the installation "Gitea base URL" must be adjusted according to the URL.

## SSH
If ssh is also to be used with Gitea, the ssh port must be exposed as a dedicated port.
Note that the ssh port is also used by the host by default.