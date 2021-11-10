# Good-Eat-API
It is a RESTful API service for the food ordering service. Clients can choose their favorite restaurant to order the food and the restaurant owners can update their menu with this service.

# Microservice Architecture
The microservice contains 7 services.

![Microservice Architecture](https://user-images.githubusercontent.com/93021154/140879850-ff2f5e51-bd0b-4d1c-a114-f87a7577bfcd.png)


> ### **API Gateway**
> It is implemented with nginx as reverse proxy and force the client to do authentication before using any services.

> ### **Authentication**
> It stores the username and password of users. It will generate the JSON Web Token (JWT) for the valid logins. All the requests via API Gateway (except /login) require valid Bearer Token in the request header.

> ### **Store**
> It is responsible for storing the restaurant basic information, for example, store_id and store_name.

> ### **Menu**
> It is responsible for storing the menu of the restaurant. For example, menu_id, 
menu_name, and price. It also adopts the CQRS pattern, the PUT/PATCH/POST or updated related event will all be handled in the menu-write-service. The query is handled by the menu-read-service and will eventually be consistent with the write-service database.

> ### **Restaurant**
> It is a service for checking the restaurant information, menu, and the restaurant status (OFFLINE, ONLINE). It stores the status of restaurants only. It will send the menu-update event via the event bus to the Menu service.

> ### **Order**
> It is a service for storing the order information by the client. All the ordering request will be handled by this service, but not responsible for the order status (like accepted/canceled by the restaurant).

> ### **Tracking**
> It is responsible for tracking the order status (like accepted/canceled by the restaurant).

> ### **Centralized logging**
> It collects the logs of the various microservices. 
