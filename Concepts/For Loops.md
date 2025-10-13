## Key Facts

- Go only has for loops (no while loops)
- No parentheses around conditions
- Opening brace must be on same line as `for`

## Syntax

Standard for loop:

```go
for i := 0; i < len(os.Args); i++ {
    // loop body
}
```

Range-based for loop:

```go
for index, value := range slice {
    // loop body
}
```

Infinite loop:

```go
for {
    // runs forever
}
```

## Where I Learned This

- [[1.2 Command-Line Arguments]]

## Related Concepts

- [[Slices]]
- [[Control Flow]]