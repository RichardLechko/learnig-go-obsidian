## Chapter

[[1.7 Web Server]]

## Purpose

Minimal echo server that returns the URL path

## Code

```go
package main

import (
	"fmt"
	"log"
	"net/http"
)

func main() {
	http.HandleFunc("/", handler)
	log.Fatal(http.ListenAndServe("localhost:8000", nil))
}

func handler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "URL.Path = %q\n", r.URL.Path)
}
```

## Concepts Used

- [[net/http Package]] - `http.HandleFunc()`, `http.ListenAndServe()`
- [[HTTP Handlers]]
- [[log Package]] - `log.Fatal()`
- [[http.Request]] - `r.URL.Path`
- [[http.ResponseWriter]] - `w`

## How It Works

1. Main connects "/" path to handler function
2. Starts server listening on port 8000
3. When request arrives, handler echoes back the URL path

## Usage

```bash
go run main.go
# Visit http://localhost:8000/hello in browser
# Output: URL.Path = "/hello"
```