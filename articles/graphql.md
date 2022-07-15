# QRAPHQL

[предотвращаем боль и страдания](https://github.com/nodkz/graphql-rules-ru/tree/master/docs)

## Types 

1. Scalar  
1.1 Int   
1.2 Float  
1.3 String  
1.4 Boolean  
1.5 ID (serialized as a String)
2. Object (a.k.a. Record)  

### Special root operation types:
1. Query
2. Mutation
3. Subscription.


```graphql
type Book {
  id: ID!
  title: String
  author: String
}
```
3. Input (used to create or update object)
```graphql
input Book {
  title: String
  author: String
}
```
4. Enum (used to represent a fixed set of values)
```graphql
enum AllowedColor {
  RED
  GREEN
  BLUE
}
```
5. Union
```graphql
union SearchResult = Book | Author

type Book {
  ...
}

type Author {
  ...
}

type Query {
  search(contains: String): [SearchResult!]!
}
```
6. Interface

