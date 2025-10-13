## Chapter

[[1.2 Command-Line Arguments]]

## Task

Experiment to measure the difference in running time between potentially inefficient versions and the one that uses `strings.Join`

## Code

```go
package main

import (
	"fmt"
)

func main() {
	fmt.Println("come back to this later")
}
```

## Status

⚠️ Skipped - need to learn more about:

- [[time Package]] (Section 1.6)
- [[Benchmark Tests]] (Section 11.4)

## TODO

- Come back after reading Section 1.6 and 11.4
- Implement benchmark comparison
- Compare string concatenation vs `strings.Join()`