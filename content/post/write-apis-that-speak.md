+++
date = "2016-10-02T17:09:14-05:00"
draft = false
title = "Write APIs that speak"
+++

Over the course of past nine months, I have written quite a few RESTful APIs from scratch and have learned quite a bit in the process. I'll try to give a brief summary of what I learned.

It's impossible to discuss web APIs without mentioning the new contender, GraphQL. I don't believe the criticsms on REST by GraphQL proponnents are just, though. REST is more unopinionated than GraphQL since it only prescribes the method of data and does not dictate how the communication must happen. GraphQL can boast to have more features because the implementors have to conform to it's predefined data structure over HTTP, which enables it to do more out of the box. If we only introduce some structure around REST we will achieve a lot of the said benefits of GraphQL without subscribing to some of it's esoteric ideas.

And this can be done if we can only rethink our usage of **query parameters**.

Query parameters, although having the word `query` in it, does not have anything query like. The only operator it accepts is the equal operator, which limits it severely because the consumers have more needs than just equality check. I have seen people often resorting to defining special parameters that holds both an operation and column on which the data to be checked upon, like `maxAge` or `searchTitle`. If we can introduce more operators like greater than, less than etc on query parameters, we can do a whole lot more with the endpoints.

**The first step in building a more expressive API is to build a contract around query parameters.**

All the query parameters we send to our backend fall in one of the following buckets <a href='{{< relref "post/write-apis-that-speak.md#one" >}}'>[1]</a>

1. **filters**: return data that satisfy some conditions
2. **include**: include some related data 
3. **page**: used to limit the number of returned results
4. **sort**: order the data in ascending or descending order mentioned by this field
5. **fields**: return only the fields mentioned 

Let's talk about filters.

If the client and server agrees to a specific format of query parameters, where the server accepts the operation type, operation and the value, then you add a lot to the query parameter vocabulary. For defining a parameter, instead of plain `column_name=value`, we can follow the following method <a href='{{< relref "post/write-apis-that-speak.md#two" >}}'>[2]</a>: 

`where[column_name:operation]=value`

example:

`api.moviestore.com/movies?where[gross_income:lt]=100000&where[released:gt]=20160503&sort=-released`

In the above API call we are requesting for movies that have made less than 100,000 since May 03, 2016. Imagine how easy it is to understand from the backend what the api consumer is requesting.

Following such method opens up a world of possibilities to the consumers and the api providers. You can do all the arithmatic, matching and containing operation on your data from client end without knowing arbitrary parameter names. You can do even custom filtering, for instance for searching in titles(full text search), you could define the word `search` as operation in the contract.Then in the backend you can decide what you want to do with it.

`api.moviestore.com/movies?where[title:search]=madmax`

For `include`, we can define a seperate array where we gather the related data to the current endpoint that the user want to be included.

`page` is an object that has two properties. One is `page[size]` and the other is `page[number]`.

`sort` is a string that takes the column name according to which the data must be sorted. Takes a dash before the value to indicate descending order.

Here's how a complete example would look like,

`api.moviestore.com/movies?where[title:search]=max&where[gross_income:lt]=10000&include=[actors]&page[size]=10&page[number]=0&sort=-released`

What more can we do with it?

**What if we taught our backend to build queries from query parameters?**.

Look closer:

*filters* is WHERE </br>
*include* is JOIN </br>
*page* is LIMIT </br>
*sort* is ORDER </br>
*fields* is SELECT

You can write a pretty powerful query constructor from the above data that will enable the client to speak with the database. The client can request and conversate with the API according to it's need without explicit backend logic doing that for it. Of course you should never trust client sent data and beware of SQL injection so make sure the query you are executing is safe.

In my [next post](#), I'll write about how we can implement such API with the help of [objection-js](https://github.com/Vincit/objection.js/) and an excellent plugin to it, [objection-find](https://github.com/Vincit/objection-find/).

</br>
</hr>
<small><a name="one"></a>1. I picked up query categorizing from [this discussion](https://github.com/TryGhost/Ghost/issues/5463) in [Ghost](https://ghost.io). Ghost also has it's own filter query language called [gql](https://github.com/TryGhost/GQL).</small>

<small><a name="two"></a>2. The filter language has been picked up verbatim from [objection-find](https://github.com/TryGhost/Ghost/issues/5463)</a></small>
