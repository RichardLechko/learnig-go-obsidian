## Purpose

Prevents race conditions by ensuring only one goroutine accesses a variable at a time

## Syntax

```go
var mu sync.Mutex

mu.Lock()
count++
mu.Unlock()
```

## Key Points

- Use `Lock()` before accessing shared variable
- Use `Unlock()` after done accessing
- Only one goroutine can hold the lock at a time

## Where I Learned This

- [[1.7 Web Server]] (Server v2)

## Related Concepts

- [[Goroutines]]
- [[Race Conditions]]
- [[Concurrency]]
- [[sync Package]]

## Code Examples

- [[Server v2 - Echo and Counter]]