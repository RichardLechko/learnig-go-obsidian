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

	// fmt.Println(strings.Join(os.Args[1:], " "))
	// this is a good way for formatting

	fmt.Println(os.Args[1:])
	// this is the most optimal if we do not care about formatting
}
```

## Concepts Used

- [[os Package]] - `os.Args`
- [[Slices]] - `os.Args[1:]`

## Notes

- Most optimal version if formatting doesn't matter
- Can use `strings.Join()` for better formatting
- Simplest implementation