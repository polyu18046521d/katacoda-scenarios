## API Server (Flask)
The API server is responsible for providing the API services. The auth-service, restaurant-service, store-service, menu-service, tracking service, and order service are API server and currently accept the GET and POST method requests.

For demo purpose, you can bypass the auth and load services, and directly access the restaurant-service using the command: `curl --location --request GET 'localhost:5101/00001'`{{execute T1}}