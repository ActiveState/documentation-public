---
title: "Getting Started Guide"
date: 2019-12-13
weight: 1
---

You can use the ActiveState Platform API to define repeatable, composable, serverless builds.

## Tutorial

Step-by step instruction on how to start a project. The tutorial is written for developers without GraphQL experience.

The tutorial covers:

* Authentication
* Connecting to the GraphQL endpoint
* Your first query
* Understanding mutations
* Exploring the capabilities of the API

## Quick Start

A one page summary of how to start a new project.

## Where do I go next?

<table>
    <tr>
        <th>Section</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>**How do I...**</td>
        <td>Quick answers for how to accomplish some specific common tasks with the ActiveState GraphQL API.</td>
    </tr>
    <tr>
        <td>Explore the API</td>
        <td>Use the GraphiQL IDE to explore the schema and your data.</td>
    </tr>
    <tr>
        <td>Builder deep dive</td>
        <td>Dive deeper into the docs and learn about the technologies underpinning the Builder.</td>
    </tr>
</table>

<hr>

## Misc Notes

Open Source communities can use our GraphQL API to create repeatable serverless builds. Using only GraphQL queries, contributors can define and compose build steps for building complex Open Source software for any operating system and language without having to worry about infrastructure.

The GraphQL API provides a method to declare a rule that takes some set of inputs, runs a shell script or other executable, and creates some output. Rules can be composed together. An output from one rule can be used as the input to others, much like unix command line tools can be piped. 

You use the API to:

* Describe how to build things
* Specify the dependancies of those things
* Define the platforms they should be built with

### Where to begin

If you:

* Have never used GraphQL before: [About GraphQL](#about-graphql)
* Want to jump in with concrete examples: [Making API Calls](#)
* Want to try it out and experiment: [Explorer](/explorer) 

### GraphQL fundamentals

"In its simplest form, GraphQL is all about asking for specific fields of objects."

"The GraphQL query language defines how to interact with data using GraphQL's queries and mutations. Queries let you ask for data, whereas Mutations let you write data."

Key benefits of GraphQL:

* **Optimized resource usage** - The client can request the specific information and only that information. This contrasts with REST APIs which typically require multiple calls to the server that return more than the specific information required. GraphQL reduces both the number of requests and responses, and the size of the requests and responses, in many cases.
* **Easier to work with for the client** - Similarly, when the client is able to just request the required information there is less work for the client to do to parse and use the response. Clients can ask for exactly the data they need.
* **Enables better documented APIs** - Zero configuration API documentation.  

"One of the great advantages of GraphQL over REST is fetching nested resources in a single query. You can ask for a resource, for example users, and a list of nested resources, for example pins, in a single query. In order to do that with REST, you would have to get users and pins in separate HTTP requests."

"Note that only fields with Object type can have nested fields."

"GraphQL servers expose their schema in order to let clients know which queries and mutations are available."

"GraphQL defines two special object types, Query and Mutation. They are special because they define the entry points of a schema. Being the entry point of a schema means that GraphQL clients must start their queries with one or more of the fields from Query."

"Every field has an underlying function (called resolver) that runs before returning its value, so it makes sense to think of field arguments the same way we think of function arguments."


### Why we chose GraphQL

* It is a language for representing graphs, and our build system is a DAG which is a type of graph.
* It has a powerful type system and schemas
* It is widely supported and many frameworks exist that make implementing it straightforward for client applications and on the server
* It provides documentation and tooling to simplify understanding the capablities of the API and exploring it interactively.

### Testing command output

```shell
$ pip install gql
```

```python
from gql import ggl, Client
from gql.transport.requests import RequestsHTTPTransport
```

```json
{
  "me": {
    "name": "Luke Skywalker"
  }
}
```

## Additional resources

- [GraphQL spec](https://graphql.github.io/graphql-spec/June2018/)
- [GraphQL implementations and documentation examples](https://github.com/APIs-guru/graphql-apis)
- [GraphQL resources](https://github.com/chentsulin/awesome-graphql)
- [Inventory API slides](https://github.com/ActiveState/presentations/blob/master/inventory-api-v1/index.md)
- [A gentle introduction to GraphQL API integrations](https://codewithhugo.com/a-gentle-introduction-to-graphql-api-integrations/)
- [Explore Your GraphQL Server in the Browser with GraphiQL](https://medium.com/hootsuite-engineering/explore-your-graphql-server-in-the-browser-with-graphiql-c3ee53745f9)

### Static sites

- [Dynamic JAMStack with Gatsby and Hasura GraphQL](https://blog.hasura.io/dynamic-jamstack-with-gatsby-hasura-graphql/)
