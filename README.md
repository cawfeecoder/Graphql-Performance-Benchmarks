# Graphql-Performance-Benchmarks
WIP: Performance Benchmarks Across Major GraphQL Server Libraries in Various Languages

Currently Comparing:

| Language | Library              | Database | Proxied | Proxy Server Language | Proxied Server Library | Status           |
| -------- | -------------------- | -------- | ------- | --------------------- | ---------------------- | ---------------- |
| Elixir   | Phoenix + Absinthe   | Rethink  | N/A     | N/A                   | N/A                    | In-Progress      |
| Golang   | Iris                 | Rethink  | Yes     | NodeJS                | Express + GraphQL      | In-Progress      |

Note: This is currently a WIP. The longterm aim is to get a comparison between all supported GraphQL Languages and 
Server Library Implementations

Quick Notes Comparing Golang to Phoenix:

- It appears up to ~100-200 records(nested, single join), the proxied Golang and Phoenix will take approximately the same time.
- I still need to saturate both servers and see what happens, test LB, etc.
- Around ~1000 records, the NodeJS server chokes and takes 1.3-1.5s for the return, Phoenix appears to cap at 600-700ms
- This indicates that good practice using GraphQL Pagination(utilizing Connections) should be used in production to limit 
query time to a minimum. The ideal size for a "page" would ideally be less than 100 and probably greater than or equal to 10.
The aim is to strive for a MAX of 50ms time to return a query

Why GraphQL?

https://0x2a.sh/from-rest-to-graphql-b4e95e94c26b

TLDR: While REST APIs provide action based organization of resources and effectively use JSON and Request Parameters to perform
these actions, we are often returning data that we don't need at the time(bloat). GraphQL ensures that the client is requesting
only the data it needs, in the JSON format it expects. Moreover, it takes care of the whole meta-philosophical problem of the
client having to know what data it needs ahead of time during development(providing GraphQL queries allows a client a bit of
free reign - within a permissions/restruction metholodogy - to get the data it needs without the development process of
exponential increasing API endpoints). Moreover, we live in an age of instant gratification... anything that makes an application
render faster/more efficently is paramount to owning the user experience. Plus, if you provide a "proxying" server for the GraphQL requests, you can do interesting things with data resolution(microservice architecture, etc.)

NodeJS Proxy Impl: https://github.com/nfrush/healthcare-graphql-express-http2
Golang Backend Impl: https://github.com/nfrush/graphql-healthcare-iris
Elixir Phoenix w/ Absinthe Impl: https://github.com/nfrush/healthcare-phoenix-graphql
Elixir Backend Impl:
