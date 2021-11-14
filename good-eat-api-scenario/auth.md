All the HTTP request from clients to the API Gatewy requires authentication. The authentication is implemented by the JSON Web Token (JWT).

The JWT will be generated when you input the correct username and password in the login stage. The JWT should be included in the authentication header as Bearer Token. The API Gateway will go to the /verify endpoint to verify the validity of the token.

### To get a JSON Web Token
`curl -H "Content-Type: application/json" --request POST -d '{ "username": "test", "password": "test" }' http://localhost:8080/login`{{execute T1}}

It will return a JWT Token. The token will be used in the other endpoints. We can save the token into a variable.

`jwt_var=<token inside the result>`

**Important: You need to copy and paste the JWT here manually**

### To get the restaurant information with id 00001
`curl -H "Authorization: Bearer $jwt_var" --request GET http://localhost:8080/eats/00001`{{execute T1}}