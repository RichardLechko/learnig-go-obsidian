## Definition

Type conversion is the explicit transformation of a value from one type to another.

## Syntax

```go
TypeName(value)
```

## Basic Examples

```go
var i int = 42
var f float64 = float64(i)    // int to float64
var u uint = uint(f)           // float64 to uint
```

## Named Type Conversions

```go
type Celsius float64
type Fahrenheit float64

var c Celsius = 100
var f Fahrenheit = Fahrenheit(c*9/5 + 32)  // Celsius to Fahrenheit

var temp float64 = float64(c)   // Celsius to float64
var c2 Celsius = Celsius(temp)  // float64 back to Celsius
```

## Key Rules

### 1. Conversions Must Be Explicit

```go
var i int = 42
var f float64 = i  // ✗ compile error: cannot use i (type int) as type float64

var f float64 = float64(i)  // ✓ explicit conversion required
```

### 2. Conversions Never Fail at Runtime

Go's type system ensures that if a conversion compiles, it will succeed at runtime. However:

- Numeric conversions may lose precision
- Conversions may truncate values

```go
var f float64 = 3.14
var i int = int(f)  // i = 3 (truncated, but doesn't fail)
```

### 3. Conversions Between Compatible Types

You can convert between types when:

- They have the same underlying type
- Both are numeric types
- One is a string and the other is []byte or []rune

## Numeric Type Conversions

```go
var i int = 1000
var i8 int8 = int8(i)      // May overflow
var u uint = uint(i)        // Sign change
var f float64 = float64(i)  // Precision may change
```

**Warning:** Converting large values to smaller types may cause overflow:

```go
var i int = 1000
var i8 int8 = int8(i)  // i8 = -24 (overflow!)
```

## String Conversions

### String to []byte

```go
s := "hello"
b := []byte(s)  // []byte{'h', 'e', 'l', 'l', 'o'}
```

### String to []rune

```go
s := "hello"
r := []rune(s)  // []rune{104, 101, 108, 108, 111}
```

### []byte to String

```go
b := []byte{'h', 'i'}
s := string(b)  // "hi"
```

### Integer to String

```go
i := 65
s := string(i)  // "A" (converts to Unicode character, not "65"!)
```

**Important:** To convert integer to its string representation, use `strconv`:

```go
import "strconv"

i := 42
s := strconv.Itoa(i)  // "42"
```

## Conversions with Same Underlying Type

Types with the same underlying type can be converted:

```go
type Age int
type Year int

var age Age = 25
var year Year = Year(age)  // ✓ Both have underlying type int
```

## Cannot Convert Between Unrelated Types

```go
type Point struct{ X, Y int }
type Coordinate struct{ X, Y int }

var p Point
var c Coordinate = Coordinate(p)  // ✗ compile error
```

Even though they have the same structure, they are unrelated types.

## Conversions vs Assertions

**Type Conversion:** For compatible types, checked at compile time

```go
var i int = 42
var f float64 = float64(i)  // Conversion
```

**Type Assertion:** For interface types, checked at runtime

```go
var i interface{} = 42
var n int = i.(int)  // Assertion
```

## Common Conversions

```go
// Integer conversions
int8, int16, int32, int64 ↔ int
uint8, uint16, uint32, uint64 ↔ uint

// Float conversions
float32 ↔ float64

// String conversions
string ↔ []byte
string ↔ []rune

// Named type conversions
CustomType ↔ UnderlyingType
```

## Best Practices

1. **Be explicit** - Go requires explicit conversions for safety
2. **Watch for overflow** - converting to smaller types may lose data
3. **Understand precision loss** - float to int truncates decimal
4. **Use strconv for strings** - don't use `string(int)` for number-to-string

## Where I Learned This

- [[2.5 Type Declarations]]

## Related Concepts

- [[Named Types]]
- [[Underlying Type]]
- [[Type Assertions]]
- [[strconv Package]]