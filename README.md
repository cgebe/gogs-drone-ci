# gogs-drone-ci

## Configuration

## SSL Certificate and Key

Use an officially signed SSL Certificate and Key
* Place the key and cert file inside /nginx as `nginx.key` and `nginx.crt`
* Comment out `DRONE_GOGS_SKIP_VERIFY=true` inside `docker-compose.yml`

Or generate certificate and key by your own:
* `sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /nginx/nginx.key -out /nginx/nginx.cert`

## Set Server IP or Domain Name
* Change the {SERVER_IP} for **each** server_name inside the `/nginx/nginx.conf` file:

E.g. 
```
    server {
        listen 80;
        server_name 46.101.223.213;
        ...
    }
```

## Drone Secret

* Change the {DRONE_SECRET} inside `docker-compose.yml` to a secure string of your choice

## Docker Registry

* When not in need of a docker registry, comment out the registry block inside `docker-compose.yml` and the server directive with port 5443 inside `nginx.conf`
* Otherwise create a htpassword file and place it as `registry.password` in /nginx. This will be authenticated users for the registry


# Services
```
    Gogs on Port 443
    Drone on Port 8443
    Registry on Port 5443
```
* HTTP Traffic on port 80 gets redirected to port 443