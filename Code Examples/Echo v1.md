## Chapter

[[1.2 Command-Line Arguments]]

## Code

```go
package main

import (
	"fmt"
	"os"
)

func main() {
	
	var s, sep string

	for i := 1; i < len(os.Args); i++ {
		s += sep + os.Args[i]
		sep = " "
	}
	fmt.Println(s)
}
```

## Concepts Used

- [[os Package]] - `os.Args`
- [[For Loops]] - traditional C-style loop
- [[Variables]] - `var s, sep string`
- [[Slices]] - `os.Args`

## What It Does

Prints command-line arguments separated by spaces