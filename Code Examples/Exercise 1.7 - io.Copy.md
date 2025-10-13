## Chapter

[[1.5 Fetching a URL]]

## Task

Use `io.Copy(dst, src)` instead of `ioutil.ReadAll` to copy response body to `os.Stdout` without requiring a large buffer

## Code

```go
package main

import (
	"fmt"
	"net/http"
	"os"
	"io"
)

func main() {
	
	for _, url := range os.Args[1:] {
		resp, err := http.Get(url)

		if err != nil {
			fmt.Fprintf(os.Stderr, "fetch: %v\n", err)
			os.Exit(1)
		}
		b, err := io.Copy(os.Stdout, resp.Body)
		resp.Body.Close()

		if err != nil {
			fmt.Fprintf(os.Stderr, "fetch: reading %s: %v\n", url, err)
			os.Exit(1)
		}

		fmt.Printf("%v", b)
	}
}
```

## Concepts Used

- [[io Package]] - `io.Copy()`
- [[Error Handling]]
- [[Streaming]] - no large buffer needed

## What Changed

- Replaced `ioutil.ReadAll()` with `io.Copy(os.Stdout, resp.Body)`
- More memory efficient for large responses
- Streams data instead of buffering entire response