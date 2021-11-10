## Circuit Breaker Pattern
It prevents a single or multiple failure of services will have a cascading effect to other normal and working microservices.

Current settings of the circuit breaker: OPEN when there is 5 continuous failure of the connections. Retry the connection after 3 seconds.

To demo the usage of circuit breaker, we stop the store-service by:

`docker stop store-load-balancer`{{execute T1}}

Send a GET request: 

`curl --location --request GET 'localhost:5110/00001'`{{execute T1}}

> Output:\- status code: 504 \- message: Service Error

If you try few more times, the status code will become 503 with message "Service is currently not available" and the response time is faster than the first HTTP requset.