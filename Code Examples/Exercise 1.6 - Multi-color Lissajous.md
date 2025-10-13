## Chapter

[[1.4 Animated GIFs]]

## Task

Modify the Lissajous program to produce images in multiple colors

## Code Changes

```go
var palette = []color.Color{color.White, color.Black, color.RGBA{00, 99, 00, 99}}

const (
	whiteIndex = 0
	blackIndex = 1
	greenIndex = 2
)
```

In the loop:

```go
img.SetColorIndex(size+int(x*size+0.5), size+int(y*size+0.5), blackIndex)
img.SetColorIndex(size+int(x*size+10), size+int(y*size+10), greenIndex)
```

## Concepts Used

- [[Composite Literals]] - adding to palette slice
- [[Constants]] - multiple color indices
- `SetColorIndex()` - setting pixel colors

## What Changed

- Added green color to palette
- Added `greenIndex` constant
- Called `SetColorIndex()` twice with offset to create multi-colored effect

## Full Code

See [[Lissajous v1]] for base implementation