TC_API_002 – POST /login – Successful login

Module: API Testing

Request Type: POST
Endpoint: /login

Body (JSON):
{
  "email": "valid@example.com",
  "password": "ValidPassword123"
}

Steps:
1. Open Postman
2. Set request type to POST
3. Enter endpoint: /login
4. Add JSON body with valid credentials
5. Click Send

Expected Result:
- Status code: 200 OK
- Response contains authentication token
- Message: “Login successful”

Priority: High
Status: Not executed
