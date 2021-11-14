## Load Balancers
Optimize the response time and avoid unevenly overloading some compute nodes while other compute nodes are left idle.

> ## Good Practice (Availability, Scalability)
> We easily scale out the service by creating more instances (e.g. Creating more docker containers, and add them into the load balancers list). When some instances of the service are down, we still have other instances as backups to support the service. It makes the service is still able to handle the user's requests.

In our service, it is implemented with the NGINX.

You can see the config of the load balancer of menu service by:

`cat ./load-balancers/menu/nginx.conf`{{execute T1}}