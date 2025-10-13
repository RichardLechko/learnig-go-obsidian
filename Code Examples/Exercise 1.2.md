## Chapter

[[1.2 Command-Line Arguments]]

## Task

Modify the echo program to print the index and value of each of its arguments, one per line

## Code

```go
package main

import (
	"fmt"
	"os"
)

func main() {

	for i := 0; i < len(os.Args); i++ {
		fmt.Printf("Arg: %s at Index %d\n", os.Args[i], i)
	}
}
```

## Concepts Used

- [[os Package]] - `os.Args`
- [[For Loops]] - traditional loop with index
- [[Printf Format Specifiers]] - `%s` and `%d`

## Output Format

```
Arg: ./program at Index 0
Arg: hello at Index 1
Arg: world at Index 2
```