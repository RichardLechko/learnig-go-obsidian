## Chapter

[[1.3 Finding Duplicate Lines]]

## Purpose

Reads a file into memory in one big gulp and then splits it by lines

## Code

```go
package main

import (
	
	"fmt"
	"os"
	"strings"
)

func main() {
	counts := make(map[string]int)

	for _, filename := range os.Args[1:] {
		data, err := os.ReadFile(filename)

		if err != nil {
			fmt.Fprintf(os.Stderr, "dup3: %v\n", err)
			continue
		}

		for _, line := range strings.Split(string(data), "\n") {
			counts[line]++
		}
	}

	for line, n := range counts {
		if n > 1 {
			fmt.Printf("%d\t%s\n", n, line)
		}
	}
}
```

## Concepts Used

- [[Maps]] - `make(map[string]int)`
- [[Error Handling]] - `os.ReadFile()` error checking
- [[strings Package]] - `strings.Split()`
- Type conversion - `string(data)`

## Differences from v2

- Reads entire file at once with `os.ReadFile()`
- Uses `strings.Split()` to break into lines
- Simpler but uses more memory
- No streaming - loads full file