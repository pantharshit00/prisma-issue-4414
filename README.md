### Introduction

Reproduction for https://github.com/prisma/prisma/issues/4414

To reproduce:-

1. Clone the repo and deploy the datamodel

2. Run the following mutation to seed some data:

```graphql
mutation {
  a: createUser(data: { name: "Harshit Pant" }) {
    id
  }
  b: createUser(
    data: { name: "Harshit Pant", relation: { create: { field: "test" } } }
  ) {
    id
  }
}
```

3. Run the following query to reproduce(Observe the aggregate count):

```graphql
{
  usersConnection(
    where: { name_contains: "Harshit", relation: { field_contains: "t" } }
  ) {
    aggregate {
      count
    }
    edges {
      node {
        id
      }
    }
  }
}
```
