## Definition

Tuple assignment allows multiple variables to be assigned at once in a single statement.

## Key Behavior

All right-hand side expressions are evaluated **first**, then all assignments are made. This is crucial for operations like swapping.

## Syntax

Basic tuple assignment:

```go
x, y = 1, 2
```

Swapping values:

```go
x, y = y, x
```

Array element swap:

```go
a[i], a[j] = a[j], a[i]
```

## Functions Returning Multiple Values

Tuple assignment is commonly used with functions that return multiple values:

```go
f, err := os.Open("file.txt")
```

## The "ok" Idiom

Many Go operations return a value and a boolean "ok" status:

```go
v, ok := m[key]     // map lookup
v, ok := x.(T)      // type assertion
v, ok := <-ch       // channel receive
```

## Discarding Values

Use the blank identifier `_` to discard unwanted values:

```go
_, err := io.Copy(dst, src)  // discard byte count
_, ok := x.(T)               // check type, discard value
```

## Best Practice

- Use tuple assignment for simple operations
- For complex situations, use sequential assignments for better readability

## Where I Learned This

- [[2.4 Assignments]]

## Related Concepts

- [[Multiple Return Values]]
- [[Blank Identifier]]
- [[Error Handling]]