## Chapter

[[1.2 Command-Line Arguments]]

## Code

```go
package main

import (
	"fmt"
	"os"
)

func main () {
	s, sep := "", ""

	for _, arg := range os.Args[1:] {
		s += sep + arg
		sep = " "
	}

	fmt.Println(s)
}
```

## Concepts Used

- [[os Package]] - `os.Args`
- [[For Loops]] - range-based loop
- [[Slices]] - `os.Args[1:]`
- Short variable declaration - `:=`

## Improvements Over v1

- Uses range loop (more idiomatic)
- Uses short variable declaration
- Blank identifier `_` to ignore index