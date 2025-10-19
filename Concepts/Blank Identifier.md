## Definition

The blank identifier `_` is used to discard values you don't need.

## Syntax

```go
_
```

## Common Uses

### Discarding Function Return Values

```go
_, err := io.Copy(dst, src)    // keep error, discard byte count
```

### Discarding in Loops

```go
for _, value := range slice {  // discard index, keep value
    fmt.Println(value)
}

for index, _ := range slice {  // keep index, discard value
    fmt.Println(index)
}
```

### Type Assertions

```go
_, ok := x.(T)  // check if x is of type T, discard the value
```

### Import Side Effects

```go
import _ "database/sql/driver"  // import for side effects only
```

## Key Properties

- Write-only variable
- Can be assigned any value of any type
- Cannot be read
- Tells the compiler you're intentionally ignoring a value

## Why Use It?

Go requires you to use all declared variables. The blank identifier lets you:

- Satisfy Go's "no unused variables" rule
- Make your intentions explicit
- Keep code clean and compilable

## Where I Learned This

- [[1.2 Command-Line Arguments]]
- [[2.4 Assignments]]

## Related Concepts

- [[Tuple Assignment]]
- [[For Loops]]
- [[Error Handling]]