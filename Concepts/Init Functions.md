## Definition

A special function that runs automatically when a package is initialized, before `main` begins execution.

## Syntax

```go
func init() {
    // initialization code
}
```

## Key Characteristics

1. **No parameters** - cannot accept arguments
2. **No return values** - cannot return anything
3. **Cannot be called** - never called explicitly by code
4. **Cannot be referenced** - cannot take its address or refer to it
5. **Automatic execution** - runs automatically at program startup

## When It Runs

- After all package-level variables are initialized
- Before `main` function begins
- In the order they appear in the source code

## Multiple init Functions

You can have multiple `init` functions:
- In a single file
- Across multiple files in the same package
- They execute in the order they're declared

```go
func init() {
    fmt.Println("First init")
}

func init() {
    fmt.Println("Second init")
}

// Output:
// First init
// Second init
```

## Common Uses

### 1. Pre-computing Lookup Tables

```go
var pc [256]byte

func init() {
    for i := range pc {
        pc[i] = pc[i/2] + byte(i&1)
    }
}
```

### 2. Registering Components

```go
func init() {
    sql.Register("postgres", &PostgresDriver{})
}
```

### 3. Configuration Setup

```go
var config Config

func init() {
    config = loadConfiguration()
}
```

### 4. Validation

```go
func init() {
    if runtime.GOOS != "linux" {
        log.Fatal("This program requires Linux")
    }
}
```

## Package Initialization Order

1. Import dependencies are initialized first
2. Package-level variables are initialized (in dependency order)
3. `init` functions run (in declaration order)
4. Process repeats for each package
5. `main` package is initialized last

## Example

```go
package main

import "fmt"

var globalVar = initGlobalVar()

func initGlobalVar() int {
    fmt.Println("Initializing global variable")
    return 42
}

func init() {
    fmt.Println("First init function")
}

func init() {
    fmt.Println("Second init function")
}

func main() {
    fmt.Println("Main function")
}

// Output:
// Initializing global variable
// First init function
// Second init function
// Main function
```

## Import for Side Effects

Sometimes you import a package only for its `init` function:

```go
import _ "image/png"  // registers PNG format in init()
```

The blank identifier `_` means "import for side effects only."

## Best Practices

### ✓ Good Uses
- Pre-computing tables
- Registering plugins/drivers
- One-time setup
- Validation checks

### ✗ Avoid
- Complex logic (hard to test)
- Order-dependent initialization across packages
- Side effects that should be explicit

## Where I Learned This

- [[2.6 Packages and Files]]

## Related Concepts

- [[Package Initialization]]
- [[Package-Level Declarations]]
- [[Blank Identifier]]
- [[Side Effects]]