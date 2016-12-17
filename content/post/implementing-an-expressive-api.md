+++
date = "2016-11-25T17:09:14-05:00"
draft = true
title = "Building a Dynamically Queryable API"
+++

*A seed project implementing all of the methods mentioned here and much more can be found [here](https://github.com/afm-sayem/ground-zero)*

To understand why I suggest building an API where the client can send arbitrary query to the backend, read this.

Today we'll build a subset of [IMDB](http://www.imdb.com/)s API.

To get started, we'll use the latest node.js(7.x) because we are going to use `async-await`. Also install PostgreSQL. If you are looking to use a different database, then look up in objection's documentations.

Install dependencies `npm install --save express body-parser pg objection objection-find knex --save`

Let's create file called app.js that will be the entry point to our express server. 
