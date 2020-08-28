# Potluck  Planner - Backend
## Deployed Backend: 
## Built With
- Node.js - JavaScript runtime for executing JavaScript at the     server outside the browser

- Express.js - Lightweight web framework to bootstrap Node.js APIs

- SQLite3 - Super lightweight database to bootstrap development environments

- PostgreSQL - An advanced object-relational database for production environments

Knex.js - A SQL query builder that helps abstracting migrations and 
DDLs for different database types into a single coherent structure

Bcrypt.js - A module to help make passwords more secure

CORS - A Node.js package for providing a Connect/Express middleware that can be used to enable CORS with various options

Helmet - A collection of 14 smaller middleware functions that set 
HTTP response headers

JWT - JSON Web Token for authorization and client side tokens for security

Supertest - A test module for HTTP assertions

Jest - A simple JavaScript testing framework

Dotenv - a zero-dependency module that loads environment variables from a .env file into process.env

## Endpoints

General
JWT protected (header) ✔️
A JWT protected endpoint means that a header object, which contains a key called Authorization with the value being a JSON web token, must be passed along with the API call in order to gain access to the endpoint.

{
  headers: {
    Authorization:
      "",
  }
}

## GET [API RUNNING]


- JWT protected (header)
- payload (body)

## API Running Response (200 OK):

{
  "message": "Server up and running!"
}


## POST [REGISTER A USER]

- JWT protected (header) ❌
payload (body) ✔️
USER gets validated over requiresAuth middleware


Example Request Body:

{
  "username": "user", // required
  "password": "password", // required
  "firstName": "test", // required
  "lastName": "test" // required
}

Register a User Response (201 CREATED):

{
  "id": 19,
  "message": "Welcome user!",
  "token": "
}

## Server Error Response (500 SERVER ERROR):

{
    "message": "Error occurred while registering a user.",
  "error": error
}

## POST [LOGIN A USER]

JWT protected (header)

payload (body) 

Example Request Body:

{
  "username": "user", // required
  "password": "password", // required
}
Example Request Body:

Login a User Response (200 OK):

{
  "id": 19,
  "message": "Welcome user!",
  "token": ""
}
Unauthorized Response (401 UNAUTHORIZED):

{
  "message": "Invalid credentials."
}
Server Error Response (500 SERVER ERROR):

{
  "message": "Error occurred while logging in a user.",
  "error": error
}
Potlucks
GET [POTLUCK BY ID]

JWT protected (header) ✔️
payload (body) ❌
ID is defined over the used route at the end
Authorization gets validated over restricted middleware
POTLUCK ID gets validated over validatePotluckData middleware
Get Event By Id Response (200 OK):

{
    "firstName": "Harry",
    "lastName": "Potter",
    "name": "potluck1",
    "location": "home",
    "time": "06:10:00",
    "date": "2020-11-25T00:00:00.000Z",
    "guests": [
        {
            "id": 3,
            "firstName": "Albus",
            "lastName": "Dumbledore",
            "accepted": true
        },
        {
            "id": 5,
            "firstName": "Ginny",
            "lastName": "Weasley",
            "accepted": false
        }
    ]
}
Server Error Response (500 SERVER ERROR):

{
  "message": "DB error. Try again.",
  "err": err
}
Event Not Found Response (500 SERVER ERROR):

{
  "message": `There was an error in getting data from the database.`,
  "err": err
}
GET [POTLUCKS BY USER ID(ORGANIZER)]
Get all the potlucks organized by a user


Response - An array of all the potlucks organized by a particular user

GET [POTLUCKS BY USER ID(ORGANIZER)]
Get all the potlucks a user is attending as a guest - GET


Query string isAttending to be provided with a value true

Response - An array of all the putlucks a user is attending

GET [POTLUCKS BY USER ID(ORGANIZER)]
Get all potlucks for which the user has not yet responded to invitations


Query string isAttending to be provided with a value false

POST [ADD A POTLUCK]

payload (body) ✔️
Example Request Body:

{
  "name": "Friendsgiving", // required
  "location": "password", // required
  "date": "11/23/2019", // required (mm/dd/yy)
  "time": "5pm" // required
}
Add a Potluck Response (201 OK):

{
  "id": 1,
  "user_id": "19",
  "name": "Friendsgiving",
  "location": "2121 Maple St, Cameron Park CA",
  "date": "11/23/2019",
  "time": "5pm"
}
Server Error Response (500 SERVER ERROR):

{
  "message": "The potluck could not be created.",
  "error": error
}
PUT [UPDATE A POTLUCK]

JWT protected (header) ✔️
payload (body) ✔️
ID is defined over the used route at the end
Authorization gets validated over restricted middleware
POTLUCK gets validated over validatePotluckData middleware
Example Request Body:

{
  "name": "Friendsgiving", // required
  "location": "2121 Maple St, Cameron Park CA", // required
  "date": "11/23/2019", // required (mm/dd/yy)
  "time": "6pm" // required
}
Updating an Event Response (201 CREATED):

{
  "id": 1,
  "user_id": "19",
  "name": "Friendsgiving",
  "location": "2121 Maple St, Cameron Park CA",
  "date": "11/23/2019",
  "time": "6pm"
}
Server Error Response (500 SERVER ERROR):

{
  "message": "The potluck could not be updated",
  "err": err
}
DELETE [POTLUCK BY ID]

JWT protected (header) ✔️
payload (body) ❌
ID is defined over the used route at the end
Authorization gets validated over restricted middleware
POTLUCK ID gets validated over validatePotluckData middleware
Delete Potluck By Id Response (200 OK):

{
  message: `The potluck was deleted.`,
}
Server Error Response (500 SERVER ERROR):

{
  "message": "The potluck could not be deleted'",
  "err": err
}