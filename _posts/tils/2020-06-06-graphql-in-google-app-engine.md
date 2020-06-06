---
layout: tils_layout
title:  "GraphQL Invalid IAP credentials: empty token"
excerpt: "Google App engine + Apollo GraphQL Invalid IAP credentials: empty token"
author: sondh5
categories: [ TILs, Gcloud, GraphQL ]
status: public
---

**Tech stacks:**
- Google app engine with Identity-Aware Proxy turned on
- GraphQL with Apollo Server Express

**Problem**
- Cannot enable playground in production
- [Appolo Docs](https://www.apollographql.com/docs/apollo-server/testing/graphql-playground/#enabling-graphql-playground-in-production)

```javascript
const { ApolloServer } = require('apollo-server');
const { typeDefs, resolvers } = require('./schema');

const server = new ApolloServer({
  typeDefs,
  resolvers,
  introspection: true,
  playground: true,
});

server.listen().then(({ url }) => {
  console.log(`🚀 Server ready at ${url}`);
});
```

**Cause**
- Request POST `/graphql` return 401 errors <br>
Digging in that request we got `"credentials": "omit"`

**Solution**
```javascript
...

const server = new ApolloServer({
  typeDefs,
  resolvers,
  introspection: true,
  playground: {
    settings: {
      'request.credentials': 'include'
    }
  },
});

...
```
