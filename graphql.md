#Graph QL
- new API Standard, alternate to REST
  - efficient, powerful and flexible
  - REST is static, GraphQL is dynamic
- flexible interface based on schema and request
- one endpoint for everything - only queries and mutations - replacing all GET, POST, POT....
- instead of controllers we have resolvers
- resolver has the same name as the query
- database agnostic, interacts with models just as well as any API
- tell the structure of my data, tell what you want using queries, get the result that perfectly matches what we require



### why important?
- strongly typed - decreases accidental errors
- also much better readibility
- error handling also easier if the issue in the type (missing name)
- defines what comes in and what comes out, guarantees that the data looks as we expect it

## Queries and mutations
- Queries and mutations are used to send and retrieve data through network requests.
- They have parameters and return values, similarly to regular functions.
- The GraphQL interface provides flexibility for the client to specify what data is needed for each request, whereas a REST API enforces strict routes.
- define name, inputs and outputs
- personalize the response data
- query and mutation are very similar, but with mutation we need to add the `mutation` keyword
```
// two queries, first gets all teams, second gets only the team with given id
type Query {
  getTeams: [Team]!
  getTeam(id: ID): Team!  // this is defined in resolvers, just like a controller
}
```
```
type Mutation {
    addTeam(team: TeamInput!): Team!
}
// input team type different than our defined Team
input TeamInput {
    name: String!
    location String!
}
```
## Resolvers
- Resolvers are where the db querying logic lives and determine how each request is handled.
- You can have resolvers for queries, mutations and types, and their naming is important.
- comparable to controllers
- takes 4 arguments
  - object - the previously resolve obj, starting value is null
  - args - arguments for the field in the query
  - context - shared object provided to every resolver
  - info - extra info about current query, field name or schema
- can return null or undefined, array (if defined), promise (graph ql can resolve promise)
```
getTeams (obj, {id}, context, info) {
    return Team.find({_id: id})
}
```

## Types
- GraphQL provides its own type system. It comes with basic scalar types such as Int and String, however, you can also create your own types.
- Each parameter and return value of a query or mutation must have a type assigned to it.
- A strongly typed code environment is more reliable and less prone to bugs.
- types are used to define the schema
- ! indicates that field is required, otherwise optional
```
type Player {
    name: String!
    age: Int!
    team: Team!
    position: [Position]!  // array of Positions
}

type Team {
    name: String!
    players: [Player]!
}

type Position...
```

- built in scalars
  - Int, Float, String, Boolean, ID
- custom types - can be specified
  - Date, Url, Email...
- each field (i.e. name, age..) can define arguments, that will add options in how it will be queried, similar to functions


