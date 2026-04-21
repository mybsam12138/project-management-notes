# API Design Specification (Extended)

## 1. Overview

This document defines the API design for the system.

-   Protocol: HTTP/HTTPS
-   Format: JSON
-   Authentication: Token-based (JWT)

------------------------------------------------------------------------

## 2. Base URL

    https://api.example.com/v1

------------------------------------------------------------------------

## 3. Authentication

### Login

**POST /auth/login**

Request:

    {
      "email": "user@example.com",
      "password": "password123"
    }

Response:

    {
      "token": "jwt-token",
      "expiresIn": 3600
    }

------------------------------------------------------------------------

## 4. User API

### Get User

**GET /users/{id}**

Response:

    {
      "id": 1,
      "name": "Sam",
      "email": "sam@example.com"
    }

------------------------------------------------------------------------

### Create User

**POST /users**

Request:

    {
      "name": "Sam",
      "email": "sam@example.com"
    }

Response:

    {
      "id": 1,
      "message": "User created"
    }

------------------------------------------------------------------------

### Update User

**PUT /users/{id}**

Request:

    {
      "name": "Updated Name",
      "email": "updated@example.com"
    }

Response:

    {
      "message": "User updated"
    }

------------------------------------------------------------------------

### Delete User

**DELETE /users/{id}**

Response:

    {
      "message": "User deleted"
    }

------------------------------------------------------------------------

## 5. Complex Query API

### Search Users

**GET /users/search**

Query Params: - name (optional) - email (optional) - page (default: 1) -
size (default: 10)

Example:

    /users/search?name=Sam&page=1&size=10

Response:

    {
      "total": 100,
      "page": 1,
      "size": 10,
      "data": [
        {
          "id": 1,
          "name": "Sam",
          "email": "sam@example.com"
        }
      ]
    }

------------------------------------------------------------------------

## 6. Command API (Action-based)

### Reset Password

**POST /users/{id}/reset-password**

Request:

    {
      "newPassword": "newPassword123"
    }

Response:

    {
      "message": "Password reset successfully"
    }

------------------------------------------------------------------------

### Activate User

**POST /users/{id}/activate**

Response:

    {
      "message": "User activated"
    }

------------------------------------------------------------------------

## 7. Error Handling

Standard Response:

    {
      "code": "ERROR_CODE",
      "message": "Error description"
    }

------------------------------------------------------------------------

## 8. Status Codes

-   200 OK
-   201 Created
-   400 Bad Request
-   401 Unauthorized
-   404 Not Found
-   500 Internal Server Error

------------------------------------------------------------------------

## 9. Naming Conventions

-   Use plural nouns: /users
-   Use lowercase
-   Use hyphen if needed

------------------------------------------------------------------------

## 10. Versioning

-   Version in URL: /v1/
-   Future: /v2/

------------------------------------------------------------------------

## 11. Security

-   HTTPS only
-   JWT authentication
-   Input validation

------------------------------------------------------------------------

## 12. Notes

-   All APIs are stateless
-   Pagination required for list APIs
