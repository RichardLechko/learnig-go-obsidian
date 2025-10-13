## Chapter

[[1.7 Web Server]]

## Purpose

Minimal HTTP reporting server that shows request details

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
	log.Fatal(http.ListenAndServe("localhost:8100", nil))
}

func handler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "%s %s %s\n", r.Method, r.URL, r.Proto)

	for k, v := range r.Header {
		fmt.Fprintf(w, "Header[%q] = %q\n", k, v)
	}
	fmt.Fprintf(w, "Host = %q\n", r.Host)
	fmt.Fprintf(w, "RemoteAddr = %q\n", r.RemoteAddr)

	if err := r.ParseForm(); err != nil {
		log.Print(err)
	}

	for k, v := range r.Form {
		fmt.Fprintf(w, "Form[%q] = %q\n", k, v)
	}
}

func counter(w http.ResponseWriter, r *http.Request) {
	mu.Lock()
	fmt.Fprintf(w, "Count %d\n", count)
	mu.Unlock()
}
```

## Concepts Used

- [[http.Request]] - Method, URL, Proto, Header, Host, RemoteAddr, Form
- [[For Loops]] - range over Header and Form maps
- [[Error Handling]] - `r.ParseForm()`
- [[Maps]] - iterating over request headers and form data

## How It Works

Reports comprehensive request information:

- HTTP method (GET, POST, etc.)
- URL and protocol
- All HTTP headers
- Host and remote address
- Form parameters if present

## Output Example

```
GET /test?name=value HTTP/1.1
Header["User-Agent"] = ["Mozilla/5.0..."]
Host = "localhost:8100"
RemoteAddr = "127.0.0.1:12345"
Form["name"] = ["value"]
```