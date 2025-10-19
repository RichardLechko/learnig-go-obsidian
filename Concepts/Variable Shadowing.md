## Definition

Variable shadowing occurs when a variable declared in an inner scope has the same name as a variable in an outer scope, temporarily hiding (shadowing) the outer variable.

## Basic Example

```go
var x = "outer"

func main() {
    x := "inner"  // Shadows the outer x
    fmt.Println(x)  // Prints: "inner"
}

func other() {
    fmt.Println(x)  // Prints: "outer"
}
```

## Multiple Levels of Shadowing

```go
var x = "package level"

func main() {
    x := "function level"
    fmt.Println(x)  // Prints: "function level"
    
    if true {
        x := "block level"
        fmt.Println(x)  // Prints: "block level"
    }
    
    fmt.Println(x)  // Prints: "function level"
}
```

## For Loop Shadowing

```go
func main() {
    x := "hello"
    
    for _, x := range x {      // x #2: loop variable (rune)
        x := x + 'A' - 'a'     // x #3: block variable
        fmt.Printf("%c", x)
    }
    // x #1: still contains "hello"
}
```

Three different variables all named `x`:

1. Function level: the string "hello"
2. Loop variable: each rune from the string
3. Loop body: modified rune value

## Common Pitfall: Unintended Shadowing

### Problem

```go
var cwd string

func init() {
    cwd, err := os.Getwd()  // ✗ Creates NEW local cwd
    if err != nil {
        log.Fatal(err)
    }
    // Package-level cwd is still empty!
}
```

### Solution

```go
var cwd string

func init() {
    var err error
    cwd, err = os.Getwd()  // ✓ Assigns to package-level cwd
    if err != nil {
        log.Fatal(err)
    }
}
```

## Shadowing with Short Declaration

Short variable declaration (`:=`) can create new variables that shadow outer ones:

```go
x := 1
fmt.Println(x)  // 1

if true {
    x := 2      // New variable, shadows outer x
    fmt.Println(x)  // 2
}

fmt.Println(x)  // 1 (outer x unchanged)
```

## Detecting Shadowing

Use `go vet` with the shadow analyzer:

```bash
go install golang.org/x/tools/go/analysis/passes/shadow/cmd/shadow@latest
go vet -vettool=$(which shadow)
```

## When Shadowing is Intentional

```go
func processFile(filename string) error {
    f, err := os.Open(filename)
    if err != nil {
        return err
    }
    defer f.Close()
    
    // Intentional shadowing to reuse 'err' variable
    data, err := io.ReadAll(f)
    if err != nil {
        return err
    }
    
    // Process data...
    return nil
}
```

## When Shadowing is Problematic

```go
func buggyCode() {
    done := false
    
    if condition {
        done := true  // ✗ Shadows outer done, doesn't modify it!
        fmt.Println(done)
    }
    
    fmt.Println(done)  // Still false!
}
```

**Fix:**

```go
func fixedCode() {
    done := false
    
    if condition {
        done = true  // ✓ Assigns to outer done
        fmt.Println(done)
    }
    
    fmt.Println(done)  // Now true
}
```

## Best Practices

### ✓ Acceptable Shadowing

- Reusing common names like `err` in different blocks
- Loop variables with common names like `i`, `v`
- Intentional shadowing for clarity

### ✗ Avoid

- Shadowing that makes code confusing
- Accidentally shadowing package-level variables
- Shadowing when you meant to modify outer variable

## Where I Learned This

- [[2.7 Scope]]

## Related Concepts

- [[Scope]]
- [[Lexical Blocks]]
- [[Short Variable Declaration]]
- [[Name Resolution]]