## Chapter

[[2.2 Declarations]]

## Code

```go
// Boiling prints the boiling point of water
package main

import (
	"fmt"
)

const boilingF = 212.0

func main() {

	var f = boilingF
	var c = (f - 32) * 5 / 9

	fmt.Printf("Boiling point = %gF or %gC\n", f, c)
}
```

## Concepts Used

- [[Package Declaration]] - `package main`
- [[Import Declarations]] - `import "fmt"`
- [[Package-Level Declarations]] - `const boilingF`
- [[Local Declarations]] - `var f` and `var c` inside main
- [[Constants]] - `boilingF`
- [[Variables]] - `f` and `c`

## Scope Demonstration

- `boilingF` is **package-level** → can be used in other .go files in same directory
- `f` and `c` are **local** → only accessible in `main` function

## Related Concepts

- [[Scope]]
- [[2.2 Declarations]]