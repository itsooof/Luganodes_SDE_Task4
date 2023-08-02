#User Management Dashboard

Node-UM is a user management application built using Node.js and TypeScript to help administrators manage user identities. It includes features for password resets, user creation and provisioning, user blocking and deletion. The application utilizes permission-based access control and operates in a stateless manner using JWT (JSON Web Tokens) for authentication.
Key Features

    Written in TypeScript

    Permission-based access control

    Stateless (JWT)

    User:
        Login
        Logout
        Get Own Info (By Token)
        Change Own Info
        Change Own Password
        Reset Password (Generates Token To send it to user email)

    Admin:
        Get All Users
        Get User By ID
        Add New User
        Edit User
        Delete User (Soft Delete)
        Login As User
        Get All Groups
        Get Group By Group ID
        Add Group
        Edit Group
        Delete Group (Soft)
        Get All Permissions

Tech Stack

Node-UM uses the following open-source projects to function:

    node.js
    TypeScript
    Express
    Mongodb
    Mongoose
    Joi
    jsonwebtoken

Docker Installation

If you have Docker and Docker Compose installed, follow these commands to start the application on port 8082:

bash

$ tsc
$ docker-compose up

Installation

Node-UM requires Node.js, TypeScript, and Mongodb to be installed on your system.

    Install the dependencies and devDependencies:

bash

$ npm install

    Import the DB Collections from the DB folder.

    Start the server:

bash

$ npm start

Environment Variables

You can customize the application's behavior by changing the environment variables in the .env file.

    PORT: HTTP Server Port
    HOST: HTTP Server HOST
    DB_URL: Mongodb URL
    POOL_SIZE: DB connection pool size
    JWT_ACCESS_SECRET_KEY: JSON Web Token Access Secret Key
    JWT_REFRESH_SECRET_KEY: JSON Web Token Refresh Secret Key
    ACCESS_TOKEN_EXP_TIME: Access token expiration time
    REFRESH_TOKEN_EXP_TIME: Refresh token expiration time
    RESET_PASSWORD_EXP_TIME: Reset Password Token Expiration Time (in milliseconds)

API Documentation

For all API requests (URL & JSON body), please check the Postman Collection provided.
Authentication

    Client sends a login request to the server.
    Server returns access & refresh tokens.

For all subsequent requests:

    Client sends the access token in the Authorization header.
    Server returns the response.

If the access token expires:

    Client sends a refresh token request to the server.
    Server returns a new access & refresh token.

Authorization

Node-UM validates all requests against the permissions table. If the URL doesn't exist in the permissions table, it means that it's a public URL, and any user can access it without authorization (useful for GUI static pages).

All records in the permissions table specify whether the URL requires only a token for access or both a token and specific permissions.
Permission Table Schema:

    path: HTTP URL. URLs can be static or dynamic. For dynamic URLs like "get user by ID /users/123456789", replace the dynamic string with a question mark to be "/users/?".
    method: HTTP Method (e.g., GET, POST, PUT, DELETE)
    isDefault: Set this flag to true if the path does not require users to have permission to access it (e.g., get own info, change own password)
