# TypeScript Design Patterns

## Description
Essential TypeScript design patterns and advanced type techniques for building scalable, type-safe applications.

## Advanced Types
### Discriminated Unions
```typescript
type Shape =
  | { kind: 'circle'; radius: number }
  | { kind: 'rectangle'; width: number; height: number }

function area(shape: Shape): number {
  switch (shape.kind) {
    case 'circle': return Math.PI * shape.radius ** 2
    case 'rectangle': return shape.width * shape.height
  }
}
```

### Template Literal Types
```typescript
type EventName = `on${Capitalize<string>}`
type CSSProperty = `--${string}`
```

### Conditional Types
```typescript
type NonNullable<T> = T extends null | undefined ? never : T
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : never
```

## Patterns
### Builder Pattern
```typescript
class QueryBuilder<T> {
  private filters: Array<(item: T) => boolean> = []

  where(predicate: (item: T) => boolean): this {
    this.filters.push(predicate)
    return this
  }

  execute(data: T[]): T[] {
    return data.filter(item => this.filters.every(f => f(item)))
  }
}
```

## Best Practices
1. Prefer `unknown` over `any`
2. Use `as const` for literal types
3. Leverage generic constraints
4. Use branded types for type safety
