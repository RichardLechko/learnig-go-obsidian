## Definition

Concurrent function execution

## Key Facts

- Lightweight threads managed by Go runtime
- `func main()` is itself a goroutine
- Use `go` keyword to start a new goroutine

## Syntax

```go
go fetch(url, ch)
```

## Where I Learned This

- [[1.6 Fetching URLs Concurrently]]

## Will Learn More

- [[Chapter 8 - Concurrency]]

## Related Concepts

- [[Channels]] - how goroutines communicate
- [[Concurrency]]
- [[Mutex]] - prevents race conditions

## Code Examples

- [[Fetchall]]