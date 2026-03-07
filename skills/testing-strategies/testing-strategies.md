# Testing Strategies

## Description
Comprehensive testing strategies covering unit tests, integration tests, and end-to-end testing with modern frameworks.

## Testing Pyramid
```
    /  E2E  \        Few, slow, expensive
   / Integration \   Some, moderate
  /   Unit Tests   \ Many, fast, cheap
```

## Unit Testing with Vitest
```typescript
import { describe, it, expect, vi } from 'vitest'

describe('calculateTotal', () => {
  it('applies discount correctly', () => {
    const result = calculateTotal(100, 0.2)
    expect(result).toBe(80)
  })

  it('handles edge cases', () => {
    expect(calculateTotal(0, 0.5)).toBe(0)
    expect(calculateTotal(100, 0)).toBe(100)
  })
})
```

## Integration Testing
```typescript
describe('User API', () => {
  it('creates and retrieves user', async () => {
    const created = await api.post('/users', { name: 'Alice' })
    const fetched = await api.get(`/users/${created.id}`)
    expect(fetched.name).toBe('Alice')
  })
})
```

## E2E with Playwright
```typescript
test('user login flow', async ({ page }) => {
  await page.goto('/login')
  await page.fill('[name=email]', 'user@test.com')
  await page.fill('[name=password]', 'password')
  await page.click('button[type=submit]')
  await expect(page.locator('.welcome')).toBeVisible()
})
```
