## Chapter

[[1.4 Animated GIFs]]

## Task

Change the Lissajous program's color palette to green on black

## Code

```go
var palette = []color.Color{color.Black, color.RGBA{00, 99, 00, 99}}

const (
	whiteIndex = 0
	blackIndex = 1
)
```

## Concepts Used

- [[Composite Literals]] - `color.RGBA{}`
- [[Constants]]
- Color representation in hex

## What Changed

- Changed `color.White` to `color.Black` for background
- Changed `color.Black` to green using `color.RGBA{00, 99, 00, 99}`
- Color format: `#RRGGBB` → `{0xRR, 0xGG, 0xBB, 0xff}`

## Full Code

See [[Lissajous v1]] for complete implementation