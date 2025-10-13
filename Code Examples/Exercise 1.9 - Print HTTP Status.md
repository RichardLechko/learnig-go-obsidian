## Chapter

[[1.5 Fetching a URL]]

## Task

Modify fetch to also print the HTTP status code, found in `resp.Status`

## Code

```go
package main

import (
	"fmt"
	"os"
	"strings"
	"io"
	"net/http"
)

func main() {

	s := "http://"
	if strings.HasPrefix(os.Args[1], s) == false {
		os.Args[1] = "http://" + os.Args[1]
	}
	
	for _, url := range os.Args[1:] {
	
		resp, err := http.Get(url)

		fmt.Printf("HTTP Status Code of %s\n", resp.Status)

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

- [[net/http Package]] - `resp.Status`
- [[Printf Format Specifiers]]

## What Changed

- Added `fmt.Printf("HTTP Status Code of %s\n", resp.Status)`
- Prints status before processing body
- Shows status codes like "200 OK", "404 Not Found", etc.