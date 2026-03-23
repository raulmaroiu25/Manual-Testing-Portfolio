TC_API_003 – POST /register – Create new user

Module: API Testing

Request Type: POST
Endpoint: /register

Body (JSON):
{
  "username": "newuser",
  "email": "newuser@example.com",
  "password": "StrongPass123"
}

Steps:
1. Open Postman
2. Set request type to POST
3. Enter endpoint: /register
4. Add JSON body with valid registration data
5. Click Send

Expected Result:
- Status code: 201 Created
- Response contains new user ID
- Message: “User created successfully”

Priority: High
Status: Not executed
