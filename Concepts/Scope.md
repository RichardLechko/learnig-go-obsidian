## Definition

The region of code where a name can be accessed

## Types of Scope in Go

### Package-Level Scope

```go
package main

const boilingF = 212.0  // Package-level

func main() {
    // Can use boilingF here
}

func otherFunc() {
    // Can also use boilingF here
}
```

- Declared outside any function
- Accessible in all .go files in the same directory/package

### Function-Level (Local) Scope

```go
func main() {
    var f = boilingF  // Local to main
    var c = (f - 32) * 5 / 9  // Local to main
    
    // f and c only exist inside main
}

func otherFunc() {
    // CANNOT access f or c here
}
```

- Declared inside a function
- Only accessible within that function

## Where I Learned This

- [[2.2 Declarations]]

## Related Concepts

- [[Variable Declarations]]
- [[Packages]]
- [[Functions]]

## Code Examples

- [[Boiling Point Example]]