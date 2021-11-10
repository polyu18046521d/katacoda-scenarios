To get more familiar with the microservice, we can try different API endpoints to do some basic tasks first.

Our microservice currently provide these API endpoints:
> POST /login - login the service 
>
> GET /eats/<store_id> - get the menu, store name, opening status of a restaurant
>
> POST /eats/<store_id>/menu - update the menu of a restaurant
>
> POST /eats/order - create a order
>
> GET /eats/order/<order_id> - check the order

All the microservice requires authentication, and we need to login to get the JWT (JSON Web Tokens) by using the `/login` endpoints.

`
curl -H "Content-Type: application/json" \
  --request POST \
  -d '{ "username": "test", "password": "test" }' \
  http://localhost/login
`{{execute T1}}

It will return a JWT Token. The token will be used in the other endpoints. We can save the token into a variable.

`JWT_VAR=<token inside the result>`

**Important: You need to copy and paste the JWT here manually**


## To get the restaurant information with id 00001
`curl --location --request GET 'localhost/eats/00001' \
  --header 'Authorization: Bearer $JWT_VAR'`{{execute T1}}


## To add a new menu on the store 00001
`curl --location --request POST 'localhost/eats/00001/menu' \
  --header 'Authorization: Bearer $JWT_VAR' \
  --header 'Content-Type: application/json' \
  --data-raw '{
      "menu_id": "D",
      "name": "Set Lunch D",
      "price": "150"
  }'`{{execute T1}}

