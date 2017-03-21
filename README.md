# gogs-drone-ci

This project sets up nginx, gogs, drone and a docker registry with ssl on a single machine.

## Requirements

* [Docker](https://docs.docker.com/engine/installation/linux/)
* [Docker-Compose](https://docs.docker.com/compose/install/)

## Configuration

## SSL Certificate and Key

Use an officially signed SSL Certificate and Key
* Place the key and cert file inside /nginx as `nginx.key` and `nginx.crt`
* Comment out `DRONE_GOGS_SKIP_VERIFY=true` inside `docker-compose.yml`

Or generate certificate and key by your own:
* `sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /nginx/nginx.key -out /nginx/nginx.cert`

## Replacements
* Change the `{SERVER_IP}` for **each** server_name inside the `/nginx/nginx.conf` file:

E.g. 
```
    server {
        listen 80;
        server_name 46.101.223.213;
        ...
    }
```

* Change the `{DRONE_SECRET}` inside `docker-compose.yml` to a secure string of your choice
* When not in need of a docker registry, comment out the registry block inside `docker-compose.yml` and the server directive with port 5443 inside `nginx.conf`
* Otherwise create a htpassword file and place it as `registry.password` in /nginx. This will be authenticated users for the registry

# Important

* When activating a project in drone, a webhook is created inside the gogs repository. One has to replace the address prefix from https://your-server-address:8443/hook?access_token=... to http://drone-master:8000/hook?access_token=... in the project settings in order to get the hook working.


# Usage
## Start
Run `docker-compose up` inside the project directory. This will start all services.

## Ports
```
Gogs on Port 443
Drone on Port 8443
Registry on Port 5443
```
* HTTP Traffic on port 80 gets redirected to port 443
