## Chapter

[[1.5 Fetching a URL]]

## Purpose

Prints the content found at a URL

## Code

```go
package main

import (
	"fmt"
	"net/http"
	"os"
	"io/ioutil"
)

func main() {
	
	for _, url := range os.Args[1:] {
		resp, err := http.Get(url)

		if err != nil {
			fmt.Fprintf(os.Stderr, "fetch: %v\n", err)
			os.Exit(1)
		}
		b, err := ioutil.ReadAll(resp.Body)
		resp.Body.Close()

		if err != nil {
			fmt.Fprintf(os.Stderr, "fetch: reading %s: %v\n", url, err)
			os.Exit(1)
		}

		fmt.Printf("%s", b)
	}
}
```

## Concepts Used

- [[net/http Package]] - `http.Get()`
- [[Error Handling]] - multiple error checks
- [[io Package]] - `ioutil.ReadAll()`
- Resource management - `resp.Body.Close()`

## How It Works

1. Loops through URLs from command-line
2. Makes HTTP GET request
3. Reads response body
4. Closes response body
5. Prints content