# User Registration Endpoint

## Endpoint
`POST /users/register`

## Description
This endpoint is used to register a new user. It validates the input data, hashes the password, creates a new user in the database, and returns an authentication token along with the user data.

## Request Body
The request body should be a JSON object with the following fields:
- `fullname`: An object containing:
  - `firstname`: A string with a minimum length of 3 characters (required)
  - `lastname`: A string with a minimum length of 3 characters (optional)
- `email`: A string representing a valid email address (required)
- `password`: A string with a minimum length of 6 characters (required)

### Example Response

- `fullname`: An object containing:
  - `firstname`: A string with a minimum length of 3 characters (required)
  - `lastname`: A string with a minimum length of 3 characters (optional)
- `email`: A string representing a valid email address (required)
- `password`: A string with a minimum length of 6 characters (required)
- `token`: A string with JWT token

```json
{
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "john.doe@example.com",
  "password": "password123"
} 
```

### Responses

#### success (201 Created)

- Description: User successfully registered.
- Body: A JSON object containing the authentication token and user data.
- Example:
```JSON
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "_id": "60d0fe4f5311236168a109ca",
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john.doe@example.com",
    "socketId": null
  }
}
```
### Validation Error (400 Bad Request)

- Description: One or more validation errors occurred.
- Body: A JSON object containing an array of error messages.
- Example:
```JSON 
{
  "errors": [
    {
      "msg": "Invalid Email",
      "param": "email",
      "location": "body"
    },
    {
      "msg": "Firstname must be 3 charcters long",
      "param": "fullname.firstname",
      "location": "body"
    },
    {
      "msg": "Password must be 6 charcters long",
      "param": "password",
      "location": "body"
    }
  ]
}
```
### Status Codes
- `201 Created`: User successfully registered.
- `400 Bad Request`: Validation errors in the input data.
### Notes
- Ensure that the `Content-Type` header is set to `application/json` when making requests to this endpoint.
- The `Authorization` header is not required for this endpoint.

# User Login Endpoint
## Endpoint
 `POST /users/login`

### Description
This endpoint is used to authenticate a user. It validates the input data, checks the user's credentials, and returns an authentication token along with the user data.

### Request Body
The request body should be a JSON object with the following fields:

`email`: A string representing a valid email address (required)
`password`: A string with a minimum length of 6 characters (required)
### Example

```JSON
{
  "email": "john.doe@example.com",
  "password": "password123"
}
```
### Responses
### Success (200 OK)
- `Description`: User successfully authenticated.
- `Body`: A JSON object containing the authentication token and user data.
### Example:
```JSON
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "_id": "60d0fe4f5311236168a109ca",
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john.doe@example.com",
    "socketId": null
  }
}
```
### Validation Error (400 Bad Request)
- `Description`: One or more validation errors occurred.
- `Body`: A JSON object containing an array of error messages.
### Example:
```JSON 
{
  "errors": [
    {
      "msg": "Invalid Email",
      "param": "email",
      "location": "body"
    },
    {
      "msg": "Password must be 6 charcters long",
      "param": "password",
      "location": "body"
    }
  ]
}
```

# User Profile endpoint

### Endpoint
`GET /users/profile`
### Description
This endpoint is used to get the profile of the authenticated user.

### Responses

#### Success (200 OK)
- `Description`: User profile retrieved successfully.
- `Body`: A JSON object containing the user data.
- `Example`:
```JSON
{
  "_id": "60d0fe4f5311236168a109ca",
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "john.doe@example.com",
  "socketId": null
}
```
# User Logout Endpoint
### Endpoint
`GET /users/logout`

### Description
This endpoint is used to log out the authenticated user. It clears the authentication token and adds it to the blacklist.

### Responses
#### Success (200 OK)
- `Description`: User logged out successfully.
- `Body`: A JSON object containing a success message.
- `Example`:
```JSON
{
  "message": "User logged out successfully"
}
```