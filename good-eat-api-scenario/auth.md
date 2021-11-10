All the HTTP request from clients to the API Gatewy requires authentication. The authentication is implemented by the JSON Web Token (JWT).

The JWT will be generated when you input the correct username and password in the login stage. The JWT should be included in the authentication header as Bearer Token. The API Gateway will go to the /verify endpoint to verify the validity of the token.

### To get a JSON Web Token
```
curl -H "Content-Type: application/json" \
  --request POST \
  -d '{ "username": "test", "password": "test" }' \
  http://localhost/login
```
{{execute T1}}

It will return a JWT Token. The token will be used in the other endpoints. We can save the token into a variable.

`JWT_VAR=<token inside the result>`

**Important: You need to copy and paste the JWT here manually**

### To get the restaurant information with id 00001
`curl --location --request GET 'localhost/eats/00001' \
  --header 'Authorization: Bearer $JWT_VAR'`{{execute T1}}