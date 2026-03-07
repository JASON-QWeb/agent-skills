# React Performance Optimization

## Description
A comprehensive skill for optimizing React application performance through memoization, code splitting, and render optimization techniques.

## When to Use
- Large React applications with complex component trees
- Apps experiencing render performance issues
- Projects requiring lazy loading and code splitting

## Key Techniques
### Memoization
- Use `React.memo()` for pure functional components
- Apply `useMemo()` for expensive computations
- Leverage `useCallback()` to prevent unnecessary re-renders

### Code Splitting
```javascript
const LazyComponent = React.lazy(() => import('./HeavyComponent'))

function App() {
  return (
    <Suspense fallback={<Loading />}>
      <LazyComponent />
    </Suspense>
  )
}
```

### Virtual Lists
For rendering large datasets, use windowing libraries:
```javascript
import { FixedSizeList } from 'react-window'

const Row = ({ index, style }) => (
  <div style={style}>Row {index}</div>
)

const VirtualList = () => (
  <FixedSizeList height={600} itemCount={10000} itemSize={35}>
    {Row}
  </FixedSizeList>
)
```

## Best Practices
1. Profile before optimizing - use React DevTools Profiler
2. Avoid premature optimization
3. Keep component state as local as possible
4. Use production builds for performance testing
