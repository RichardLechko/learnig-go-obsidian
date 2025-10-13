## Definition

Determines whether a name is visible outside its package

## Rules

### Exported (Capital letter)

```go
func Printf()      // Exported
type Point struct  // Exported
const MaxSize      // Exported
```

- Starts with capital letter
- Can be used outside its own package
- Public API

### Unexported (Lowercase letter)

```go
func helper()      // Unexported
type point struct  // Unexported
const maxSize      // Unexported
```

- Starts with lowercase letter
- Private to package
- Cannot be accessed outside package

## Example

```go
// In package fmt
func Printf()  // Exported - you can use fmt.Printf()
func format()  // Unexported - you CANNOT use fmt.format()
```

## Where I Learned This

- [[2.1 Names]]

## Related Concepts

- [[Packages]]
- [[Encapsulation]]
- [[Public vs Private]]