## Chapter

[[1.2 Command-Line Arguments]]

## Task

Modify the echo program to also print `os.Args[0]`, the name of the command that invoked it

## Code

```go
package main

import (
	"fmt"
	"os"
)

func main() {
	fmt.Println(os.Args[0:])
}
```

## Concepts Used

- [[os Package]] - `os.Args`
- [[Slices]] - `os.Args[0:]` includes command name

## What Changed

Changed from `os.Args[1:]` to `os.Args[0:]` to include the command name