## Chapter

[[1.3 Finding Duplicate Lines]]

## Purpose

Prints the text of each line that appears more than once in the standard input, preceded by its count

## Code

```go
package main

import (
	"fmt"
	"bufio"
	"os"
)

func main() {
	counts := make(map[string]int)

	input := bufio.NewScanner(os.Stdin)

	for input.Scan() {
		counts[input.Text()]++
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
- [[bufio Package]] - `bufio.NewScanner()`
- [[For Loops]] - range over map
- [[Printf Format Specifiers]] - `%d` and `%s`

## How It Works

1. Creates a map to count occurrences
2. Reads from standard input line by line
3. Increments count for each line
4. Prints lines that appear more than once