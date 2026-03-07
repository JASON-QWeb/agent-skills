# State Management Patterns

## Description
Modern React state management approaches comparing Context API, Zustand, and Jotai for different application scales.

## Zustand (Recommended)
```typescript
import { create } from 'zustand'

interface AppStore {
  count: number
  increment: () => void
  reset: () => void
}

const useAppStore = create<AppStore>((set) => ({
  count: 0,
  increment: () => set(state => ({ count: state.count + 1 })),
  reset: () => set({ count: 0 }),
}))

// Usage in component
function Counter() {
  const count = useAppStore(state => state.count)
  const increment = useAppStore(state => state.increment)
  return <button onClick={increment}>{count}</button>
}
```

## Jotai (Atomic State)
```typescript
import { atom, useAtom } from 'jotai'

const countAtom = atom(0)
const doubleCountAtom = atom(get => get(countAtom) * 2)

function Counter() {
  const [count, setCount] = useAtom(countAtom)
  return <button onClick={() => setCount(c => c + 1)}>{count}</button>
}
```

## When to Use What
| Solution | Use When |
|----------|----------|
| useState | Component-local state |
| Context | Theme, auth, i18n |
| Zustand | Medium-large app state |
| Jotai | Fine-grained reactive state |
| TanStack Query | Server state |
