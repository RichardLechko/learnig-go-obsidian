## Definition

Variables that contain the address of another variable

## Syntax

Get address of variable:

```go
&var
```

Get value that pointer refers to:

```go
*var
```

## Example

```go
x := 1
p := &x         // p is a pointer to x
fmt.Println(*p) // prints 1
*p = 2          // sets x to 2
```

## Where I Learned This

- [[1.8 Loose Ends]]

## Status

Only briefly mentioned - need to learn more

## Related Concepts

- [[Memory Management]]
- [[Pass by Reference]]