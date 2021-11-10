## Event-based Arechitecture (RabbitMQ)
The event queue of the microservice is implemented with RabbitMQ. 

We have inmplemented the database per servcie pattern. Each service has its own database, and some the tasks (HTTP POST request) requires the modification of multiple services. To make the tasks become asynchronize, event queue is used to make the request become asynchronous and the data will be eventually consistent.

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
`docker stop order-api`{{execute T1}}

### To send a POST order request:
`curl --location --request POST 'localhost/eats/order' \
  --header 'Content-Type: application/json' \
  --data-raw '{
      "store_id": "00001",
      "details": [
          {
              "menu_id": "A",
              "count": 1
          }
      ]
  }'
`{{execute T1}}

### To save the order id
`OID2=<returned order id>`


### To check the recently added order:
`curl --location --request GET localhost/eats/order/$OID2
`{{execute T1}}

### Resume the order-service:
`docker start order-api`{{execute T1}}

### Check the order again:
`curl --location --request GET localhost/eats/order/$OID2
`{{execute T1}}