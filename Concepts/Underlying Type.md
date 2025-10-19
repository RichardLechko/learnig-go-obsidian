## Definition

The underlying type is the base type that a named type is built upon.

## Syntax

```go
type NewType UnderlyingType
//           ^^^^^^^^^^^^^^ This is the underlying type
```

## Examples

```go
type Celsius float64     // underlying type: float64
type Age int             // underlying type: int
type Name string         // underlying type: string
type Point struct {      // underlying type: struct{X, Y int}
    X, Y int
}
```

## What It Determines

The underlying type determines:

1. **Memory representation** - how the value is stored
2. **Available operations** - what you can do with the value
3. **Conversion rules** - how types can be converted

## Inherited Operations

A named type inherits all operations from its underlying type:

```go
type Meters float64

var m Meters = 10.5
m = m + 5.0        // ✓ Addition works (from float64)
m = m * 2          // ✓ Multiplication works (from float64)
m = m / 3          // ✓ Division works (from float64)
```

## Type Conversion Rules

Types with the same underlying type can be converted to each other:

```go
type Celsius float64
type Fahrenheit float64

var c Celsius = 100
var f Fahrenheit = Fahrenheit(c)  // ✓ Both have float64 as underlying type
```

But they cannot be directly assigned:

```go
var c Celsius = 100
var f Fahrenheit = c  // ✗ compile error: different types
```

## Comparison Rules

Values of a named type can be compared to:

- Other values of the same named type
- Zero value of the underlying type
- **Not** to other named types (even with same underlying type)

```go
type Celsius float64
type Fahrenheit float64

var c Celsius = 0
var f Fahrenheit = 0

fmt.Println(c == 0)          // ✓ Can compare to zero (float64 zero value)
fmt.Println(c == Celsius(0)) // ✓ Can compare to same type
fmt.Println(c == f)          // ✗ Cannot compare different named types
```

## Predeclared Types

Go's built-in types are their own underlying types:

- `int` - underlying type is `int`
- `float64` - underlying type is `float64`
- `string` - underlying type is `string`
- etc.

## Where I Learned This

- [[2.5 Type Declarations]]

## Related Concepts

- [[Named Types]]
- [[Type Declarations]]
- [[Type Conversions]]
- [[Type Safety]]