TC_API_005 – DELETE /user/{id} – Delete user by ID

Module: API Testing

Request Type: DELETE
Endpoint: /user/{id}

Steps:
1. Open Postman
2. Set request type to DELETE
3. Enter endpoint: /user/1 (or any valid ID)
4. Click Send

Expected Result:
- Status code: 200 OK or 204 No Content
- User is removed from the system
- GET /users no longer returns the deleted user

Priority: High
Status: Not executed
