## Chapter

[[1.7 Web Server]]

## Task

Modify the Lissajous server to read parameters from the URL

## Key Code Sections

### Handler

```go
http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
	j := parseInputs(r)
	lissajous(w, j)
})
```

### Parse URL Parameters

```go
func parseInputs(r *http.Request) int {
	fmt.Println(r.URL.Query())
	value := 0
	for k, v := range r.URL.Query() {
		if k == "cycles" {
			fmt.Printf("K: %v\t V: %v\n", k, v)
			value, err := strconv.Atoi(v[0])
			fmt.Println("Value ->", value)
			if err != nil {
				fmt.Println("Error -> ", err)
			}
			return value
		}
	}
	return value
}
```

### Modified Lissajous

```go
func lissajous(out io.Writer, cycleVal int) {
	// ... constants ...
	
	for t := 0.0; t < float64(cycleVal)*2*math.Pi; t += res {
		x := math.Sin(t)
		y := math.Sin(t * freq + phase)
		img.SetColorIndex(size+int(x*size+0.5), size+int(y*size+0.5), blackIndex)
	}
	
	// ... rest of code ...
}
```

## Concepts Used

- [[http.Request]] - `r.URL.Query()`
- [[strconv Package]] - `strconv.Atoi()` to convert string to int
- [[URL Parameters]]
- [[Anonymous Functions]]

## How It Works

1. Parse URL query parameters
2. Look for "cycles" parameter
3. Convert string value to int
4. Pass to lissajous function
5. Generate GIF with custom cycle count

## Usage

```bash
# Default cycles
http://localhost:8000/

# Custom cycles
http://localhost:8000/?cycles=10
```