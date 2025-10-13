## Chapter

[[1.7 Web Server]]

## Purpose

Minimal echo and counter server with mutex for thread safety

## Code

```go
package main

import (
	"fmt"
	"log"
	"net/http"
	"sync"
)

var mu sync.Mutex
var count int

func main() {
	http.HandleFunc("/", handler)
	http.HandleFunc("/count", counter)
	log.Fatal(http.ListenAndServe("localhost:8000", nil))
}

func handler(w http.ResponseWriter, r *http.Request) {
	mu.Lock()
	count++
	mu.Unlock()
	fmt.Fprintf(w, "URL.Path = %q\n", r.URL.Path)
}

func counter(w http.ResponseWriter, r *http.Request) {
	mu.Lock()
	fmt.Fprintf(w, "Count %d\n", count)
	mu.Unlock()
}
```

## Concepts Used

- [[Mutex]] - `sync.Mutex` for thread safety
- [[net/http Package]]
- [[HTTP Handlers]] - multiple handlers
- [[Race Conditions]] - prevented by mutex

## How It Works

1. Main sets up two handlers: "/" and "/count"
2. Handler increments counter with mutex protection
3. Counter displays current count with mutex protection
4. Mutex ensures only one goroutine accesses `count` at a time

## Why Mutex?

Each HTTP request runs in its own [[Goroutines|goroutine]], so multiple requests can access `count` simultaneously. The mutex prevents race conditions.

## Usage

```bash
# Visit http://localhost:8000/anything - increments counter
# Visit http://localhost:8000/count - shows current count
```