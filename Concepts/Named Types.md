## Definition

A named type is a new type created with a type declaration that has its own unique name.

## Syntax

```go
type TypeName UnderlyingType
```

## Examples

```go
type Celsius    float64
type Fahrenheit float64
type Age        int
type Meters     float64
```

## Key Properties

### 1. Distinct Identity

Even if two named types have the same underlying type, they are **not interchangeable**:

```go
type Celsius float64
type Fahrenheit float64

var c Celsius = 100
var f Fahrenheit = 100

// These are different types, even though both are float64
fmt.Println(c == f)  // ✗ compile error: type mismatch
```

### 2. Type Safety

Named types prevent accidental mixing of values:

```go
func ProcessTemperature(c Celsius) {
    // Can only pass Celsius, not any float64
}
```

### 3. Can Have Methods

Named types can have methods attached:

```go
func (c Celsius) String() string {
    return fmt.Sprintf("%g°C", c)
}
```

### 4. Inherit Underlying Type Operations

Named types can use all operations of their underlying type:

```go
var c Celsius = 100
c = c + 10        // ✓ Can use addition (from float64)
c = c * 2         // ✓ Can use multiplication
```

## Type Conversions

Must explicitly convert between named types and their underlying type:

```go
var c Celsius = 100
var f float64 = float64(c)  // Explicit conversion required
var c2 Celsius = Celsius(f)  // Explicit conversion required
```

## Benefits

1. **Self-documenting code** - type name explains what value represents
2. **Type safety** - compiler prevents mixing incompatible values
3. **Custom behavior** - can add methods specific to the type
4. **Better errors** - compiler error messages use type names

## Named Types vs Type Aliases

```go
// Named type - creates NEW type
type Celsius float64

// Type alias - just another name for same type
type Alias = float64
```

Type aliases (with `=`) create an alternate name for an existing type, not a new type.

## Where I Learned This

- [[1.8 Loose Ends]]
- [[2.5 Type Declarations]]

## Related Concepts

- [[Type Declarations]]
- [[Underlying Type]]
- [[Type Conversions]]
- [[Methods]]
- [[Type Safety]]