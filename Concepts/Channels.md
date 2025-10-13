## Definition

Communication mechanism that allows goroutines to pass values to each other

## Syntax

Create a channel:

```go
ch := make(chan string)
```

Send to channel:

```go
ch <- value
```

Receive from channel:

```go
value := <-ch
```

## Where I Learned This

- [[1.6 Fetching URLs Concurrently]]

## Will Learn More

- [[Chapter 8 - Concurrency]]

## Related Concepts

- [[Goroutines]]
- [[Concurrency]]

## Code Examples

- [[Fetchall]]