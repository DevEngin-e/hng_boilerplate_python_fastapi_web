# FASTAPI
FastAPI boilerplate

## Setup

1. Create a virtual environment.
 ```sh
    python3 -m venv .venv
 ```
2. Activate virtual environment.
```sh
    source /path/to/venv/bin/activate`
```
3. Install project dependencies `pip install -r requirements.txt`
4. Create a .env file by copying the .env.sample file
`cp .env.sample .env`

5. Start server.
 ```sh
 python main.py
```

## Overview
This API is designed for Task 3 and provides several endpoints for user authentication, organization management, payments, messaging, and general settings. The API is secured using OAuth 2.0 and JWT tokens.

For a comprehensive understanding of our project's structure and functionality, you can refer to the [API documentation](https://app.swaggerhub.com/apis-docs/KENOSAGIE88/HngTask2/1.0.0#/), which provides detailed information about our endpoints, request/response formats, and overall API design. Additionally, the [Entity-Relationship Diagram (ERD)](https://erd.dbdesigner.net/designer/schema/1720776149-task03) offers a visual representation of our database schema, illustrating the relationships between different entities within our system.


Base URL
The base URL for the API is:



**https://virtserver.swaggerhub.com/KENOSAGIE88/HngTask2/1.0.0**

Authentication
Login
Endpoint: /api/v1/auth/login
Method: POST
Summary: Creates a new user
Request Body:

```
json

{
  "email": "string",
  "password": "string"
}
```

Responses:
```
200: Successfully Logged User In
400: Bad Request
```

Google Login
Endpoint: /api/v1/auth/google/login
Method: POST
Summary: Handle Google Login Callback
Request Body:

```
json

{
  "authtoken": "string"
}
```
Responses:

```
200: Successful login
400: Invalid authorization code.

```
Logout
Endpoint: /api/v1/auth/logout
Method: POST
Summary: User logout

Responses:
```
204: User logged out successfully

```
Request Magic Link
Endpoint: /api/v1/auth/magic-link/login
Method: POST
Summary: Request Magic Link

Request Body:
```
json

{
  "email": "string"
}
```
Responses:
```
202: Magic link sent successfully.
400: Bad Request (e.g., invalid email)

```
Change Password
Endpoint: /api/v1/auth/change-password
Method: POST
Summary: Change User Password
Request Body:
```
json

{
  "current_password": "string",
  "new_password": "string"
}

```
Responses:
```
200: Password Changed Successfully
400: Bad Request
401: Former password Incorrect

```
Request Password Reset
Endpoint: /api/v1/password/reset
Method: POST
Summary: Request password reset
Request Body:
```
json

{
  "email": "string"
}

```
Responses:
```
200: Password reset email sent
404: User not found

```
Confirm Password Reset
Endpoint: /api/v1/password/reset/confirm
Method: POST
Summary: Confirm password reset
Request Body:
```

json

{
  "token": "string",
  "newPassword": "string"
}

```
Responses:
```
200: Password reset confirmed
400: Bad request

```
Superadmin
List Users
Endpoint: /api/admin/users
Method: GET
Summary: List all users
Responses:
```
200: Query Successful
{
  "status": "string",
  "message": "string",
  "data": [
    {
      "id": "string",
      "email": "string",
      "username": "string",
      "password": "string",
      "is_admin": true,
      "userDetails": {
        "id": "string",
        "height": 0,
        "age": 0,
        "profilepic": "string"
      }
    }
  ]
}
```
List Organizations
Endpoint: /api/v1/admin/organizations
Method: GET
Summary: Admin List organizations
Responses:
```
200: A list of organizations
[
  {
    "id": "string",
    "name": "string"
  }
]
```

List Payments
Endpoint: /api/v1/admin/payments
Method: GET
Summary: Admin Payments
Responses:
```
200: A list of payments
[
  {
    "id": "string",
    "amount": 0,
    "currency": "string",
    "status": "string"
  }
]
```

Get Activity Log
Endpoint: /api/v1/admin/activity-log
Method: GET
Summary: Admin Get activity log
Responses:
```
200: Activity log
[
  {
    "action": "string",
    "timestamp": "string"
  }
]


```
Messaging
Send Email
Endpoint: /api/v1/email/send
Method: POST
Summary: Send email
Request Body:
```
json

{
  "recipient": "string",
  "subject": "string",
  "message": "string"
}
```
Responses:
```
200: Email sent successfully
500: Server error
```
Payments
Stripe Payment Processing
Endpoint: /api/v1/payments/stripe
Method: POST
Summary: Stripe payment processing
Request Body:
```
json

{
  "id": "string",
  "amount": 100,
  "currency": "string"
}

```
Responses:
```
200: Payment processed successfully
400: Bad request

```
Flutterwave Payment Processing
Endpoint: /api/v1/payments/flutterwave
Method: POST
Summary: Flutterwave payment processing
Request Body:
```
json

{
  "id": "string",
  "amount": 100,
  "currency": "string"
}

```
Responses:
```
200: Payment processed successfully
400: Bad request
```

LemonSqueezy Payment Processing
Endpoint: /api/v1/payments/lemonsqueezy
Method: POST
Summary: LemonSqueezy payment processing
Request Body:
```
json

{
  "id": "string",
  "amount": 100,
  "currency": "string"
}
```
Responses:
```
200: Payment processed successfully
400: Bad request

```
List All Payments
Endpoint: /api/v1/payments
Method: GET
Summary: List all payments
Responses:
```
200: List of payments
```
Get Payment Details
Endpoint: /api/v1/payments/{id}
Method: GET
Summary: Get payment details
Responses:
```
200: Payment details
[
  {
    "id": "string",
    "amount": 0,
    "currency": "string",
    "status": "string"
  }
]
404: Payment not found
```
Organization
List All Organizations
Endpoint: /api/v1/organizations
Method: GET
Summary: List all organizations
Responses:
```
200: A list of organizations
[
  {
    "id": "string",
    "name": "string"
  }
]
```
Create Organization
Endpoint: /api/v1/organizations
Method: POST
Summary: Create organization
Request Body:
```
json

{
  "name": "string"
}
```
Responses:
```
201: Organization created successfully
400: Bad request
```
Get Organization Details
Endpoint: /api/v1/organizations/{id}
Method: GET
Summary: Get organization details
Responses:
```
200: Organization details
{
    "id": "string",
    "name": "string"
  }
404: Organization not found
```
Update Organization
Endpoint: /api/v1/organizations/{id}
Method: PUT
Summary: Update organization
Request Body:
```
json

{
  "name": "string"
}
```
Responses:
```
200: Organization updated successfully
404: Organization not found
```
Delete Organization

Endpoint: /api/v1/organizations/{id}
Method: DELETE
Summary: Delete organization
Responses:
```
204: Organization deleted successfully
403: Forbidden
404: Organization not found
```
Add User to Organization
Endpoint: /api/v1/organizations/{id}/add-user
Method: POST
Summary: Add user to organization
Request Body:
```
json

{
  "userId": "string"
}
```
Responses:
```
200: User added to organization
404: Organization or user not found

```
List User Organizations
Endpoint: /api/v1/users/{id}/organizations
Method: GET
Summary: Get a list of all user organizations
Responses:
```
200: A list of user organizations
[
  {
    "id": "string",
    "name": "string"
  }
]
404: User not found

```
Get User Organization Details
Endpoint: /api/v1/users/{userId}/organizations/{orgId}
Method: GET
Summary: Get a specific user organization
Responses:
```
200: Organization details

  {
    "id": "string",
    "name": "string"
  }

404: Organization or user not found

```
Delete User from Organization
Endpoint: /api/v1/users/{userId}/organizations/{orgId}
Method: DELETE
Summary: Delete a user from an organization
Responses:
```
204: User removed from organization
404: Organization or user not found

```
Settings
Get General Settings
Endpoint: /api/v1/settings
Method: GET
Summary: Get general settings
Responses:
```
200: General settings for logged-in user
{
  "theme": "string",
  "notificationsEnabled": true
}
```


Profile
GET 
/api/v1/profile
Get profile settings for logged in user

Responses
```
{
  "code": 200,
  "description": "User profile settings",
  "schema": {
    "type": "object",
    "properties": {
      "username": {
        "type": "string"
      },
      "email": {
        "type": "string"
      }
    }
  }
}
```
PUT 
/api/v1/profile
Update profile settings for logged in user

Request Body
```
{
  "username": "string",
  "email": "string"
}
```
Responses
```
{
  "code": 200,
  "description": "Profile updated successfully"
}
```

POST 
/api/v1/profile/avatar
Upload profile picture for logged in user

Request Body
```
multipart/form-data:
  avatar: string($binary)
```
Responses
```
{
  "code": 200,
  "description": "Avatar uploaded successfully"
}
```
