## Definition

One of the four declaration types in Go (var, const, type, func).

"A declaration names a program entity and specifies some or all of its properties" (p. 28)

## Syntax Options

### Explicit Type

```go
var s string
var i int
var f float64
```

### Type Inference

```go
var s = "hello"  // Go infers string type
var i = 42       // Go infers int type
```

### Short Variable Declaration

```go
s := "hello"     // Only inside functions
i := 42
```

## Zero Values

Uninitialized variables get zero value:

- Numbers → `0`
- Strings → `""`
- Booleans → `false`
- Pointers → `nil`

## Where I Learned This

- [[1.2 Command-Line Arguments]]
- [[2.2 Declarations]]

## Related Concepts

- [[Constants]]
- [[Type Declarations]]
- [[Scope]]

## Code Examples

- [[Echo v1]]
- [[Boiling Point Example]]