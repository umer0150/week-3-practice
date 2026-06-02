# Performance + Custom Hooks

## useMemo

```tsx
const filteredUsers = useMemo(() => {
  return users.filter((u) =>
    u.name.includes(search)
  );
}, [users, search]);
```

## useCallback

```tsx
const handleDelete = useCallback(
  (id:number) => {
    console.log(id);
  },
  []
);
```

## useRef

```tsx
const renderCount = useRef(0);

useEffect(() => {
  renderCount.current += 1;
});
```

## Custom Hook

```tsx
import { useEffect, useState } from "react";

export function useDebounce<T>(
  value: T,
  delay = 500
) {
  const [debounced, setDebounced] =
    useState(value);

  useEffect(() => {
    const timer = setTimeout(() => {
      setDebounced(value);
    }, delay);

    return () => clearTimeout(timer);
  }, [value, delay]);

  return debounced;
}
```

## Error Boundary

```tsx
class ErrorBoundary extends React.Component {
  state = { hasError: false };

  static getDerivedStateFromError() {
    return { hasError: true };
  }

  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong</h1>;
    }

    return this.props.children;
  }
}
```
