Research Guide  and Tasks for Monday:

What is GraphQL?
- A query language for reading and mutating data in APIs
- Developed by Meta
- Backend: GraphQL provides a type system where you can describe a schema for your data
    - This gives API consumers the power to explore and request the exact data that they need


GraphQL vs REST?

What are the benefits of using GraphQL building an API  when compared to REST?
1) GraphQL does't use URLs to specify the resources that are available in the API - instead it uses a GraphQL Schema.
- This allows you to send complex queries that fetch additional data according to relationships defined in the schema.
- Doing the same with REST is more complicated - it requires more queries, and the queries would need to occur on the client-side.

2) GraphQL prevents over-requesting and under-requesting of data.
- With REST -> the API responds with the total data entity from that endpoint.
    - We get all of the data from that endpoint every time, which may be more than is required for your desired action.
    - Additonally, you may often need to make multiple requests to different services in order to get all of your needed data.
- GraphQL has a single entry-point, and the consumer can define the data they want to receive.

One key risk of GraphQL is that while it allows clients to query for JUST the data they need, some queries may cause major database issues (and will require effort/resources to mitigate this risk).

3) REST is beneficial in its simplicity, because no additional libraries are required to consume an API.
- GraphQL requires heavier tooling (both client-side and server-side). This is more expensive and time-consuming.

4) REST uses HTTP GET which is easy to cache.
- GraphQL uses HTTP POST, which provides less caching upon initial setup.

In a system like REST, you can only pass a single set of arguments - the query parameters and URL segments in your request.
But in GraphQL, every field and nested object can get its own set of arguments, making GraphQL a complete replacement for making multiple API fetches.


GraphQL Foundational Topics :
- Every GraphQL service has a query type and may or may not have a mutation type. These types are the same as a regular object type, but they are special because they define the entry point of every GraphQL query.

Mutation
- If you have an API endpoint that alters data, like inserting data into a database or altering data already in a database, you should make this endpoint a Mutation rather than a Query.
    - This is as simple as making the API endpoint part of the top-level Mutation type instead of the top-level Query type.

Schema and TypesQuery
- Every GraphQL service defines a set of types which completely describe the set of possible data you can query on that service. Then, when queries come in, they are validated and executed against that schema.


GraphQL Environment

Apollo
- Apollo GraphOS is the developer platform for building a supergraph: a unified network of your organization's data and services, all composed into a single distributed GraphQL API.

Apollo Client
- Apollo Client is a comprehensive state management library for JavaScript that enables you to manage both local and remote data with GraphQL. Use it to fetch, cache, and modify application data, all while automatically updating your UI.



Using this GraphQL Playground : ​​https://users-messages-gql.herokuapp.com/graphql, get familiar with the GraphQL syntax by doing the following:
Write a query to fetch all users
```
query GetUsers{
  users {
    username
    first_name
    last_name
  }
}
```

Write a query to fetch all users and their messages
```
query GetUsersAndMessages{
  users {
    username
    first_name
    last_name
    messages {
      id
      body
      user {
        username
      }
    }
  }
}
```

Add a user
```
mutation AddUser($username: ID!, $first_name: String!, $last_name: String!) {
	createUser(username: $username, first_name: $first_name, last_name: $last_name){
    username
    first_name
    last_name
  }
}

Query Variables:
{
  "username": "jhellst",
  "first_name": "Josh",
  "last_name": "H"
}
```


Add a message
```
mutation AddMessage($id: ID!, $body: String!) {
	createMessage(username: $id, body: $body){
    id
    body
  }
}
```

Create a small React App that communicates with the above-mentioned GraphQL API. Your app should be able to do the following:
List all users
List all messages for a given user
Add an user
Add  a message
	You don’t need to use Apollo Server!!!

Research the following tools (OPTIONAL)
Apollo Rover
Graphql Codegen
