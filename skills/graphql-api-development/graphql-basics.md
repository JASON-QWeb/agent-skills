# GraphQL API Development

## Description
Building efficient GraphQL APIs with schema design, resolvers, and client-side data fetching patterns.

## Schema Definition
```graphql
type User {
  id: ID!
  name: String!
  email: String!
  posts: [Post!]!
}

type Post {
  id: ID!
  title: String!
  content: String!
  author: User!
  createdAt: DateTime!
}

type Query {
  user(id: ID!): User
  posts(first: Int, after: String): PostConnection!
}

type Mutation {
  createPost(input: CreatePostInput!): Post!
}
```

## Resolver Pattern
```typescript
const resolvers = {
  Query: {
    user: (_, { id }) => db.users.findUnique({ where: { id } }),
    posts: (_, { first, after }) => paginate(db.posts, { first, after }),
  },
  User: {
    posts: (parent) => db.posts.findMany({ where: { authorId: parent.id } }),
  },
}
```

## Client with Apollo
```typescript
const GET_USER = gql`
  query GetUser($id: ID!) {
    user(id: $id) {
      name
      posts { title }
    }
  }
`

function UserProfile({ id }: { id: string }) {
  const { data, loading } = useQuery(GET_USER, { variables: { id } })
  if (loading) return <Spinner />
  return <div>{data.user.name}</div>
}
```

## Best Practices
1. Use DataLoader to solve N+1 queries
2. Implement cursor-based pagination
3. Add query complexity limits
4. Use persisted queries in production
