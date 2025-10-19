## Definition

Lexical blocks are implicit scopes in Go that define where names can be accessed, even without explicit braces `{}`.

## Types of Lexical Blocks

### 1. Universe Block

Contains all Go source code - built-in types, functions, and constants

```go
// These are in the universe block:
int, string, bool, true, false, nil, len, append, etc.
```

### 2. Package Block

All files in a single package

```go
package main

// These declarations are in the package block:
var globalVar = 10
const Pi = 3.14

func helper() {}
```

### 3. File Block

A single .go file - mainly for imported package names

```go
package main

import "fmt"  // 'fmt' is in this file's block

func main() {
    fmt.Println("Hello")  // Can use 'fmt' here
}
```

### 4. Function Block

Each function or method

```go
func example() {
    // This entire function is a lexical block
    var x = 10
}
```

### 5. Control Flow Blocks

Each `for`, `if`, `switch`, `select` creates a lexical block

```go
for i := 0; i < 10; i++ {  // 'i' is in for statement block
    // Loop body is another nested block
}

if x := getValue(); x > 0 {  // 'x' is in if statement block
    // If body is another nested block
}
```

## Lexical Block vs Syntactic Block

### Syntactic Block

Explicitly marked with braces `{}`

```go
func main() {
    {  // <-- Explicit syntactic block
        var x = 1
    }
}
```

### Lexical Block

Implicit scope without braces

```go
for i := 0; i < 10; i++ {
    // 'i' exists in lexical block of the for statement
    // even though it's not inside the braces
}
```

## For Loop Has Two Lexical Blocks

```go
for i := 0; i < 10; i++ {  // Block 1: 'i' exists here
    var x = i * 2          // Block 2: 'x' exists here
}
// Neither 'i' nor 'x' exists here
```

## Name Resolution in Lexical Blocks

Compiler searches from innermost to outermost:

```go
var x = "package"  // Universe/Package block

func main() {      // Function block
    var x = "function"
    
    if true {      // If statement block
        var x = "if"
        fmt.Println(x)  // Prints: "if"
    }
    
    fmt.Println(x)     // Prints: "function"
}

func other() {
    fmt.Println(x)     // Prints: "package"
}
```

## Nested Lexical Blocks Example

```go
package main  // Package block

import "fmt"  // File block

var global = 1  // Package block

func example() {  // Function block
    var fn = 2    // Function block
    
    for i := 0; i < 3; i++ {  // For statement block ('i' lives here)
        var loop = 3           // For body block
        
        if true {              // If statement block
            var ifVar = 4      // If body block
            
            // Can access: global, fn, i, loop, ifVar
        }
        // Can access: global, fn, i, loop
        // Cannot access: ifVar
    }
    // Can access: global, fn
    // Cannot access: i, loop, ifVar
}
```

## Why Lexical Blocks Matter

1. **Determine variable lifetime** - when variables are created/destroyed
2. **Control name visibility** - what names are accessible where
3. **Enable shadowing** - inner blocks can hide outer names
4. **Prevent name conflicts** - same name can exist in different blocks

## Where I Learned This

- [[2.7 Scope]]

## Related Concepts

- [[Scope]]
- [[Syntactic Blocks]]
- [[Variable Shadowing]]
- [[Name Resolution]]