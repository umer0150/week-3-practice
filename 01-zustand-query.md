# Zustand + TanStack Query Practice

## Zustand Auth Store

```tsx
import { create } from "zustand";

type AuthState = {
  user: string | null;
  login: (name: string) => void;
  logout: () => void;
};

export const useAuthStore = create<AuthState>((set) => ({
  user: null,
  login: (name) => set({ user: name }),
  logout: () => set({ user: null }),
}));
```

## Query Example

```tsx
import { useQuery } from "@tanstack/react-query";

async function getUsers() {
  const res = await fetch("/api/users");
  return res.json();
}

export function Users() {
  const { data, isLoading } = useQuery({
    queryKey: ["users"],
    queryFn: getUsers,
    staleTime: 60000,
  });

  if (isLoading) return <p>Loading...</p>;

  return (
    <ul>
      {data.map((user:any) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```
