---
layout: post
title:  "Getting Started with Nodal"
date:   2015-12-23 21:28:15 +0700
categories: [JavaScript]
---

# What is Nodal?
Nodal is an ES6-native, MVC, Node.js framework for rapidly building scalable API services. It comes with a built-in ORM, migration support, its own routing system and more.

Boasting its own opinionated, explicit, idiomatic and highly-extensible framework, Nodal takes care of all of the hard decisions for you and your team. This allows you to focus on creating an effective product in a short timespan while minimizing technical debt.

# Installation
### Install Node and Nodal
If you don't have Node, install Node by going to https://nodejs.org/

```js
// we can then install Nodal globally using npm
npm install nodal -g
```

### Install Postgres

Go to http://postgresapp.com/ and download the application. 
Move the application to your applications folder and launch the application.

If you get any error messages during this tutorial, some common errors are included at end of article. 

# Creating an API server for Twitter clone
We'll be building a simple API server for a twitter clone called InstaTweet. It'll be a basic version of the APIs that allow users to create accounts, login and create content associated with their accounts like Twitter, Reddit or HackerNews.

### Create Project

```js
nodal new instatweet-api // create new nodal project called instatweet-api

cd instatweet-api // go into directory

nodal s // start nodal server

nodal help // more information in CLI commands

// NOTE: Server should running smoothly
// Ready: HTTP Worker listening on port 3000
// If you have other servers running, close them and start nodal server again

// create model called Tweet which has two fields: 
// a user_id which is an integer, and a body which is a string
```

### Create Models
One of the great things about nodal is that we can create models and controllers from terminal

```js
nodal g:model Tweet user_id:int body:string 
/* NOTE: Migrations are a convenient way to alter your database schema over time in a consistent and easy way. You don't have to write SQL by hand, allowing your schema and changes to be database independent.
*/

// You can think of each migration as being a new 'version' of the database.

// NOTE: You'll see that the Nodal generator logs the files it generates in your console.

nodal db:create // create our PostgreSQL database

nodal db:prepare // empties out our database and prepares for migration

nodal db:migrate // creates the tables in our database.
```

### Create Controllers
At this point we have a database, a tweet table in that database, a tweet model for interacting with that tweet table, and a tweet schema that describes our tweet in our model and our Postgres table. But we don't have a way to communicate with our Nodal instatweet-api externally. We need an API endpoint. For that we need to generate a controller that interfaces with our tweet model. In Nodal, we can generate controllers for specific models, and we can namespace our controllers and API endpoints, all in one command.

```js
nodal g:controller v1 --for Tweet // create controller for Tweet model
// Note: Console should log
// Create: ./app/controllers/v1/tweets_controller.js
// Modify: ./app/router.js

nodal db:migrate // creates the tables in our database.

// NOTE: Check your /v1/tweets endpoints with some POSTs and GETs

// Other Commands //
nodal db:rollback // roll's our database back to a prior migration

nodal db:migrate // roll our database forward again
```

First, we create our v1 name-spaced tweets_controller. The controllers that Nodal generates provide index, show, create, update and destroy methods, which all correspond to simple CRUD operations. The design pattern implemented here is based on frameworks like Rails.

### Router
We can see that we have a route for every controller in our API, like our index controller from the start of the tutorial. When Nodal generates a controller, it explicitly required that controller into the router and generates a route for that controller as well:

```js
  // ./app/router.js
  
  /* Routes */

  const IndexController = Nodal.require('app/controllers/index_controller.js');

  /* generator: begin imports */

  const V1TweetsController = Nodal.require('app/controllers/v1/tweets_controller.js'); // created controller

  /* generator: end imports */

  router.route('/').use(IndexController);

  /* generator: begin routes */

  router.route('/v1/tweets/{id}').use(V1TweetsController); // created route

  /* generator: end routes */

  return router;
```

As seen above, Nodal generates the controller and route for our project. It even comments where the generation begins and ends. Nodal implements routes using a regex waterfall, where requests fall through each regex until the requested url string finds a regex match.

### Test Tweet Endpoint 
Now that we've built our tweets endpoint, let's test it by sending a POST request with they word "Hey" in the body to `localhost:3000/v1/tweets`. Using Postman, we send our data using the `x-www-form-urlencoded` option. Or if you want to use curl from the command line: `curl -d "body=hey" localhost:3000/v1/tweets`
The joys of persisting data. 

```js
// testing with cURl
curl --data "user_id=0&body=hello tyrion" http://localhost:3000/v1/tweets
curl --data "user_id=0&body=hello hodor" http://localhost:3000/v1/tweets
curl --data "user_id=0&body=hello jon" http://localhost:3000/v1/tweets
curl --data "user_id=1&body=hello arya" http://localhost:3000/v1/tweets
curl --data "user_id=2&body=winter is coming" http://localhost:3000/v1/tweets
curl --data "user_id=2&body=winter is coming now" http://localhost:3000/v1/tweets
```

### Input Validation
One of the features we want to implement with our instatweet-API is input validation. That is we want to be able to reject requests to our API that have invalid input. This is an important part of maintaining an API, and Nodal makes it easy by providing input validation out of the box. We can use our tweet model to validate input using the `.validates` method, which takes as arguments:

* the field to validate

* the text string to respond with in case validation fails

* an anonymous function that will evaluate to true or false using the data in the designated input field.

Let's validate the body of our POST request to make sure that it both exists and is longer than 5 characters.

```js
// ./app/models/tweet.js

  Tweet.setSchema(Nodal.my.Schema.models.Tweet);

  Tweet.validates('body', 'must be at least 5 characters', v => v && v.length >= 5); // Add validation

  return Tweet;
```

Try sending a POST request with "Hey" in the body. We should get a validation error!

```js
{
  "meta": {
    "total": 0,
    "count": 0,
    "offset": 0,
    "error": {
      "message": "Validation error",
      "details": {
        "body": [
          "must be at least 5 characters"
        ]
      }
    }
  },
  "data": []
}
```

### Query Strings
If we hit localhost:3000/v1/tweets with a GET request, we'll get all of our tweets back to us in the body of the response.

Nodal comes with support for multiple query strings:

Here are a couple we can test:

```js
localhost:3000/v1/tweets?body__not_null
localhost:3000/v1/tweets?body__startswith=he 
// NOTE: the query is case sensitive
localhost:3000/v1/tweets?body__startswith=He
localhost:3000/v1/tweets?body__endswith=friend!
localhost:3000/v1/tweets?body__iendswith=frieNd! // iendswith for case insensitive
localhost:3000/v1/tweets?id__gte=3&__count=2 // all tweets for which the ID is greater-than-or-equal-to 3
```

## User Model and Authentication
Nodal provides a generator for creating the foundation of a user model. We can use Nodal's command line generator flag --user to generate a user model. This flag does a lot under the hood, but at this point we're equipped to reason through what Nodal generates. The Nodal command to generate a user model is:

```js
nodal g:model --user

sudo nodal g:model --user // if error, use super user

// LOGS: 
// Create: ./app/models/user.js
// Create: ./db/migrations/2016041500085963__create_user.js

nodal db:migrate // we need to migrate that model

nodal g:controller v1 --for User // create controller 
// LOGS: 
// Create: ./app/controllers/v1/users_controller.js
// Modify: ./app/router.js
```

### Test with Fake Users
You can use Postman, an app to test API endpoints. Or you can use good old Curl 

```js
curl --data "email=jonsnow@gmail.com&username=jonsnow&password=secret" http://localhost:3000/v1/users
curl --data "email=daenerys@gmail.com&username=daenerys&password=secret" http://localhost:3000/v1/users
curl --data "email=arya@gmail.com&username=arya&password=secret" http://localhost:3000/v1/users
curl --data "email=tyrion@gmail.com&username=tyrion&password=secret" http://localhost:3000/v1/users
curl --data "email=hodor@gmail.com&username=hodor&password=secret" http://localhost:3000/v1/users
```

### API Endpoint Response Interface
Our `users_controller.js` file is where we specify the response data to API requests. We can specify an interface to describe those responses. We can edit any of our responses by adding an array specifying what model data we want to send in our response. In this case we'll add `['id','username','email','created_at']` as an argument to `this.respond()` on our index method in our `users_controller.js` file, which corresponds to a GET request to `/v1/users/ endpoint`.

```js
// ./app/controllers/v1/users_controller.js

User.query()
  .where(this.params.query)
  .end((err, models) => {

    this.respond(err || models, ['id','username','email','created_at']); // attributes we want to return 

  });
```

### Hide password
To prevent accidentally showing your users secure fields (i.e. password) by mistyping, you can secure fields with Model.hides in your Model definition file.

```js
  // models/user.js
  
  User.validates('password', 'must be at least 5 characters in length', v => v && v.length >= 5);

  User.hides('password'); // hide password

  return User;
```

### Postgres Terminal Commands

```js
psql --username=postgres // launch postgres

\list or \l // list all databases 

\du // list of roles

drop database database_name; // remove PostgresSQL database 
// NOTE: Don't forget ';'

\c database_name // switch to database

// After you connect to database // 

\d // show all tables, views and sequences
\dt // show only list of tables you created

select * from tweets; // select all columns from tweets
// NOTE: Don't forget ';'

\q // quit

```

### Error Messages and How to Fix Them

```js
// error 
Error: connect ECONNREFUSED 127.0.0.1:5432 // this means that your postgres is not running
```