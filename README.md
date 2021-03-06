Maelström - Users
=================
_by @demiurgosoft_   
[![Build Status](https://travis-ci.org/demiurgosoft/maelstrom-users.svg?branch=master)](https://travis-ci.org/demiurgosoft/maelstrom-users)
[![Coverage Status](https://coveralls.io/repos/github/demiurgosoft/maelstrom-users/badge.svg?branch=master)](https://coveralls.io/github/demiurgosoft/maelstrom-users?branch=master)
[![bitHound Overall Score](https://www.bithound.io/github/demiurgosoft/maelstrom-users/badges/score.svg)](https://www.bithound.io/github/demiurgosoft/maelstrom-users)
[![bitHound Dependencies](https://www.bithound.io/github/demiurgosoft/maelstrom-users/badges/dependencies.svg)](https://www.bithound.io/github/demiurgosoft/maelstrom-users/master/dependencies/npm)

![Maelström Logo](https://raw.githubusercontent.com/demiurgosoft/maelstrom/master/logo/logo.jpg)

Users micro-service for [Mäelstrom project](https://github.com/demiurgosoft/maelstrom), login and authentication with MongoDB and JWT



## Geting Started
MongoDB required

1. To install the service and necessary dependencies: `npm install --production`
	1. If you want also the dev-dependencies (for testing and development of Mäelstrom-users): `npm install`
	2. To test the service using mocha: `npm test`
2. To start the service: `npm start`
3. Configure the system with the files under `config/` folder

To test the system, it will provide a simple login and signup clients (`/login` and `/signup`)

## API REST
Users microservice is a RESTful API with http request and json responses:

|Method|URL         |Usage   |Response|
|:----:|:----------:|:-------|:-------|
|POST|`/login`    |Logs user with given data `{"username","password"}` in the system|Returns the token `{"token"}` and code 200 or an error|
|POST|`/signup`   |Creates a new user with given data `{"username","password","email"}`if it doesn't exist|Returns the login token or an error|
|PUT |`/restricted/update`|Updates user data with given data `{"username","password"}`|Returns status 204 if everything is ok|
|DELETE|`/restricted/remove`|Removes user|204 if everything is ok|
|GET|`/restricted/dash`|Gets logged User info|code 200 and user data {"_id","username","email"}` or 400 and error log|


>All urls under `restricted/*` requires a valid token, auth header must be `Bearer [token]` to get access.


## Response status

|Code|Meaning                        |
|:--:|:------------------------------|
|201 |OK in POST operations          |
|204 |OK in PUT and DELETE operations|
|400 |Bad request (not valid body)   |
|401 |Invalid token (not authorized  |
|403 |Incorrect password             |
|404 |Data not found                 |
|500 |Internal server error          |

## JWT
The tokens used are [Json Web Tokens](http://jwt.io/) with the following payload structure:
```JSON
{
"id": "56d96ce3a5e8cf4c28e1a4a4",
"username": "my user",
...
}
```
Each user has an unique _id_ used across all the maelström servers (Mongodb id), also the username is stored. All the tokens are signed with a private key in the server (for testing use `dontpanic42`)

> Licensed under GNU AFFERO GENERAL PUBLIC LICENSE Version 3
> Maelström logo by @iblancasa under CC0
