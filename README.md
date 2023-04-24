# Apollo-Server
As explained [here](https://github.com/apollographql/apollo-server), an Apollo Server is an open-source, spec-compliant GraphQL
server that's compatible with any GraphQL client, including Apollo Client. 
It's the best way to build a production-ready, self-documenting GraphQL API that can use data from any source.
## Table of Contents:
* [Creating a project](#creating-a-project)
* [Install dependencies](#install-dependencies)
* [Defining a schema](#defining-a-schema)

## Creating a Project:
Initialize a node js project using npm init --yes && npm pkg set type="module"

### Install Dependencies:
Applications that run Apollo Server require two top-level dependencies:
1. graphql
1. @apollo/server

#### Run the following command to install them:
```
npm i graphql @apollo/server
```

### Defining a Schema
- Create a file named ***index.js*** in the root of your project folder
- Paste the following code:
```
import { ApolloServer } from "@apollo/server";
import { startStandaloneServer } from '@apollo/server/standalone'

const typeDefs = `#graphql
    type Book {
        title: String
        author: String
    }

    type Query {
        books: [Book]
    }
`

const books = [
    {
        title: "The Awekaning",
        author: "Kate Chopin"
    },
    {
        title: "City of Glass",
        author: "Paul Auster"
    }
]

const resolvers = {
    Query: {
        books: () => books
    }
}

const server = new ApolloServer({
    typeDefs,
    resolvers
})

const { url } = await startStandaloneServer(server, {
    listen : { port: 4000 },
});

console.log(`🚀  Server ready at: ${url}`);
```

*Note* Add this to the Scripts of your package.json file:
```
"start": "node index.js"
```
Then run your server with:
```
npm start
```
Execute your query by visiting the [url](http://127.0.0.1:4000)
