# Behind the scenes

## Load Balancers (NGINX)
Optimize the response time and avoid unevenly overloading some compute nodes while other compute nodes are left idle.

You can see the config of the load balancer of menu service by:

`cat ./load-balancers/menu/nginx.conf`{{execute T1}}