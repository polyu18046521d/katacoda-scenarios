##  Command and Query Responsibility Segregation (CQRS) Pattern
This pattern seperates the read and update operations. CQRS can helps in maximizing the mircoservice performance, scalability, and security.

> ## Good Practice (Scalability)
> Supports multiple denormalized views that are scalable and performant

Our menu-service is implemented with the CQRS pattern. The menu-service is divided into two services: menu-write-service (for the write operations) and menu-read-service (for the read operation).

To make sure the HTTP POST Operation is handled by the menu-write-service, and the GET operation is handled by the meni-read-service, the load balancer will redirectly all the GET operation to the menu-read-servce and all POST operation to the menu-write-service.

The written data will be pass to the event queue and the menu-read-service database will be eventually same as the menu-write-service database.

You can stop the menu-write-service by: `docker stop project-menu-write-api`{{execute T1}}
and you can still use the HTTP GET request to query the menu data

## To get the restaurant information with id 00001
`curl -H "Authorization: Bearer $jwt_var" --request GET http://localhost:8080/eats/00001`{{execute T1}}