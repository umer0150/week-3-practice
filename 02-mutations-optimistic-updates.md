# Mutations + Optimistic Updates

```tsx
const queryClient = useQueryClient();

const mutation = useMutation({
  mutationFn: createTodo,

  onMutate: async (newTodo) => {
    await queryClient.cancelQueries({ queryKey: ["todos"] });

    const previous =
      queryClient.getQueryData(["todos"]);

    queryClient.setQueryData(
      ["todos"],
      (old:any = []) => [...old, newTodo]
    );

    return { previous };
  },

  onError: (_err, _todo, context) => {
    queryClient.setQueryData(
      ["todos"],
      context?.previous
    );
  },

  onSuccess: () => {
    console.log("Success");
  },

  onSettled: () => {
    queryClient.invalidateQueries({
      queryKey: ["todos"],
    });
  },
});
```

## Exercise

- Add Todo
- Delete Todo
- Rollback on failure
- Refetch after mutation
