## Definition

Data structure that holds key/value pairs

## Performance

Provides constant-time operations to store, retrieve, or test for items

## Syntax

Create a map:

```go
counts := make(map[string]int)
```

Use a map:

```go
counts[key]++
```

## Important Notes

- Maps are references to the data structure created by `make`
- When passed to a function, the function receives a copy of the reference
- Changes made in the function are visible to the caller

## Where I Learned This

- [[1.3 Finding Duplicate Lines]]

## Code Examples

- [[Dup v1]]
- [[Dup v2]]
- [[Dup v3]]