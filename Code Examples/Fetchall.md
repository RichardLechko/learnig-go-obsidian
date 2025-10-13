## Chapter

[[1.6 Fetching URLs Concurrently]]

## Purpose

Fetches URLs in parallel and reports their times and sizes

## Code

```go
package main

import (
	"fmt"
	"io"
	"io/ioutil"
	"net/http"
	"os"
	"time"
)

func main() {

	start := time.Now()
	ch := make(chan string)

	for _, url := range os.Args[1:] {
		go fetch(url, ch)
	}

	for range os.Args[1:] {
		fmt.Println(<-ch)
	}

	fmt.Printf("%.2fs elapsed\n", time.Since(start).Seconds())
}

func fetch(url string, ch chan<- string) {
	
	start := time.Now()
	resp, err := http.Get(url)

	if err != nil {
		ch <- fmt.Sprint(err)
		return
	}

	nbytes, err := io.Copy(ioutil.Discard, resp.Body)
	resp.Body.Close()

	if err != nil {
		ch <- fmt.Sprint("while reading %s: %v", url, err)
		return
	}

	secs := time.Since(start).Seconds()
	ch <- fmt.Sprintf("%.2fs %7d %s", secs, nbytes, url)
}
```

## Concepts Used

- [[Goroutines]] - `go fetch(url, ch)`
- [[Channels]] - `ch := make(chan string)`
- [[time Package]] - timing operations
- Channel operations - send `<-` and receive `<-ch`

## How It Works

1. Main creates channel of strings
2. Starts goroutine for each URL
3. Each goroutine fetches URL and sends result to channel
4. Main receives from channel for each URL
5. Prints total elapsed time

## Key Insight

Demonstrates concurrent execution - all URLs fetched in parallel instead of sequentially