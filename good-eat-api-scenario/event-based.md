## Event-based Architecture (RabbitMQ)
The event queue of the microservice is implemented with RabbitMQ. 

We have implemented the database per service pattern. Each service has its own database, and some the tasks (HTTP POST request) requires the modification of multiple services. To make the tasks become asynchronous, event queue is used to make the request become asynchronous and the data will be eventually consistent.

For example, if you send a create order request:
> 1. Tracking service will receive the request
> 2. Tracking service will create a <order_id>
> 3. Tracking service will create a status: PENDING in its database
> 4. A 'order-updated' event will be sent to the event queue 'tracking-order-queue'
> 5. Tracking service return the <order_id>
> 6. Order service will consume the 'order-updated' event
> 7. Order service will create the new order in its database

Also, the event queue will keep the task even there is not consumers (service down), and resume when the service is up again.

### To stop the order service: 
`docker stop project-order-api`{{execute T1}}

### To send a POST order request:
`curl -H "Authorization: Bearer $jwt_var" -H "Content-Type: application/json" -d '{
      "store_id": "00001",
      "details": [
          {
              "menu_id": "A",
              "count": 1
          }
      ]
  }' --request POST http://localhost:8080/eats/order`{{execute T1}}

### To save the order id
`oid=<returned order id>`


### To check the recently added order:
`curl -H "Authorization: Bearer $jwt_var" --request GET http://localhost:8080/eats/order/$oid`{{execute T1}}

### Resume the order-service:
`docker start order-api`{{execute T1}}

### Check the order again:
`curl -H "Authorization: Bearer $jwt_var" --request GET http://localhost:8080/eats/order/$oid`{{execute T1}}