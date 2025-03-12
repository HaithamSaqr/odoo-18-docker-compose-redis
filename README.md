# Installing Odoo 18.0 with one command (Supports multiple Odoo instances on one server).

## Quick Installation

Install [docker](https://docs.docker.com/get-docker/) and [docker-compose](https://docs.docker.com/compose/install/) yourself, then run the following to set up first Odoo instance @ `localhost:10018` (default master password: `minhng.info`):

``` bash
cd /opt
curl -s https://raw.githubusercontent.com/HaithamSaqr/odoo-18-docker-compose-redis/master/run.sh | sudo bash -s odoo18 10018 20018
```
and/or run the following to set up another Odoo instance @ `localhost:11018` (default master password: `falconvalley`):

``` bash
cd /opt
curl -s https://raw.githubusercontent.com/HaithamSaqr/odoo-18-docker-compose-redis/master/run.sh | sudo bash -s odoo18 11018 21018
```


Then open `localhost:10018` to access Odoo 18.

- **If you get any permission issues**, change the folder permission to make sure that the container is able to access the directory:

``` sh
$ sudo chmod -R 777 addons
$ sudo chmod -R 777 etc
$ sudo chmod -R 777 postgresql
```

- If you want to start the server with a different port, change **10018** to another value in **docker-compose.yml** inside the parent dir:

```
ports:
 - "10018:8069"
```
check if running 
docker exec -it docker-name redis-cli ping
If Redis is running correctly, you should get:
PONG

Monitor Redis Activity in Real Time
You can use the MONITOR command inside Redis to watch real-time transactions:
$ docker exec -it docker-name redis-cli monitor


Verify Redis Configuration in Odoo
To be sure Odoo is configured to use Redis, you can check the configuration file:
$ docker exec -it odoo18 bash -c "cat /etc/odoo/odoo.conf | grep redis"

If Redis is configured properly, you should see Redis settings like:

redis_host = redis-hostname
redis_port = 6379

Check If Odoo is Connected to Redis
Run the following inside Odoo’s container to check the Redis connection:
$docker exec -it odoo18-1 bash -c "ping redis-hostname"

