# Behind the scenes
One RESTful API request is calling different microservices. For example, the GET /eats/[store-id] request is calling the auth-service, restaurant-service, store-service, and menu-service.

## API Gateway (NGINX)
All the requests from the clients will all travel to the API Gateway. It is an API management tool that sits between a client and a collection of backend services.

> Advantages:
> - Forwards the call to the appropriate services on the back end
> - Change a back-end service without breaking the client
> - Protect your APIs from overuse and abuse, so you use an authentication service and rate limiting

You can check the config of the API Gateway by:
`cat ./reverse_proxy/nginx.conf`{{execute T1}}