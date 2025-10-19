## Definition

Package initialization is the process of setting up a package's state before it can be used, including initializing variables and running `init` functions.

## Initialization Order

### Within a Single Package

1. **Import declarations** - imported packages are initialized first
2. **Package-level variables** - initialized in dependency order
3. **init functions** - executed in the order they appear

### Example

```go
package example

import "fmt"

var a = b + c  // initialized third (depends on b and c)
var b = f()    // initialized second (depends on f)
var c = 1      // initialized first (no dependencies)

func f() int {
    return c + 1
}

func init() {
    fmt.Println("Package initialized")
}
```

## Multiple Files

If a package has multiple files:

1. Go compiler sorts files by name
2. Variables across all files are initialized in dependency order
3. `init` functions from all files execute in order

```bash
# Files processed in this order:
a_config.go
b_setup.go
c_main.go
```

## Dependency Resolution

Variables are initialized based on their dependencies, not declaration order:

```go
var x = y + 1  // initialized second
var y = 1      // initialized first (y needed for x)
```

The compiler builds a dependency graph to determine correct initialization order.

## Package Dependency Order

Packages are initialized in import order:

```
main imports: [fmt, mypackage, net/http]

Initialization order:
1. fmt package
2. mypackage package
3. net/http package
4. main package
```

If package `A` imports `B`, and `B` imports `C`:

```
C is fully initialized first
Then B is fully initialized
Then A is fully initialized
```

## Complete Initialization Process

```go
package main

import (
    "fmt"
    "myapp/database"  // Initialized before main
)

var config = loadConfig()  // Initialized before init()

func loadConfig() Config {
    fmt.Println("Loading config")
    return Config{Port: 8080}
}

func init() {
    fmt.Println("First init")
}

func init() {
    fmt.Println("Second init")
}

func main() {
    fmt.Println("Main function")
}

// Output:
// [database package initialization]
// Loading config
// First init
// Second init
// Main function
```

## Initialization Timeline

```
1. Import graph is constructed
2. Packages are initialized bottom-up (dependencies first)
3. For each package:
   a. Package-level variables initialized (dependency order)
   b. All init() functions run (declaration order)
4. Finally, main.main() executes
```

## Visual Example

```
Package Structure:
main
├── imports database
│   └── imports logger
└── imports config

Initialization Order:
1. logger package
   - logger variables
   - logger init()
2. database package
   - database variables (may use logger)
   - database init()
3. config package
   - config variables
   - config init()
4. main package
   - main variables
   - main init()
   - main.main()
```

## Circular Dependencies

Go **prohibits** circular imports:

```go
// package a
import "b"  // ✗ Error if b also imports a
```

This prevents circular initialization issues.

## Initialization Guarantees

Go guarantees:

1. Each package is initialized **exactly once**
2. Variables are initialized **before** they're used
3. `init` functions run **after** all variables are initialized
4. All initialization completes **before** `main` starts

## Common Patterns

### Database Connection

```go
package database

import "database/sql"

var DB *sql.DB

func init() {
    var err error
    DB, err = sql.Open("postgres", "connection_string")
    if err != nil {
        panic(err)
    }
}
```

### Configuration Loading

```go
package config

var Settings Config

func init() {
    Settings = loadFromFile("config.json")
}
```

### Package Registration

```go
package image

import _ "image/png"  // Registers PNG decoder in init()
import _ "image/jpeg" // Registers JPEG decoder in init()
```

## Debugging Initialization

Add print statements to understand initialization order:

```go
var x = func() int {
    fmt.Println("Initializing x")
    return 1
}()

func init() {
    fmt.Println("Running init")
}

func main() {
    fmt.Println("Running main")
}

// Output:
// Initializing x
// Running init
// Running main
```

## Best Practices

### ✓ Good

- Simple variable initialization
- Loading configuration
- Registering components
- One-time setup

### ✗ Avoid

- Complex logic in init (hard to test)
- Panicking in init (crashes program at startup)
- Depending on initialization order across packages
- Side effects that should be explicit

## Where I Learned This

- [[2.6 Packages and Files]]

## Related Concepts

- [[init Function]]
- [[Package-Level Declarations]]
- [[Packages]]
- [[Import Side Effects]]