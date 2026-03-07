# Next.js App Router Patterns

## Description
Modern Next.js App Router patterns including server components, streaming, and data fetching strategies.

## Server Components
```tsx
// app/users/page.tsx - Server Component by default
async function UsersPage() {
  const users = await db.users.findMany()
  return (
    <ul>
      {users.map(user => <UserCard key={user.id} user={user} />)}
    </ul>
  )
}
```

## Loading States
```tsx
// app/users/loading.tsx
export default function Loading() {
  return <UsersSkeleton />
}
```

## Server Actions
```tsx
// app/actions.ts
'use server'

export async function createPost(formData: FormData) {
  const title = formData.get('title') as string
  await db.posts.create({ data: { title } })
  revalidatePath('/posts')
}
```

## Route Handlers
```tsx
// app/api/users/route.ts
export async function GET(request: Request) {
  const { searchParams } = new URL(request.url)
  const page = Number(searchParams.get('page') ?? 1)
  const users = await db.users.findMany({ skip: (page - 1) * 10, take: 10 })
  return Response.json(users)
}
```

## Parallel Routes
```
app/
├── @modal/
│   └── login/page.tsx
├── @sidebar/
│   └── page.tsx
└── layout.tsx
```
