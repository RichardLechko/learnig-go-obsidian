## Basic Switch

```go
switch coinflip() {
    case "heads":
        heads++
    case "tails":
        tails++
    default:
        fmt.Println("landed on edge!")
}
```

## Tagless Switch

Also called "switch true" - evaluates boolean conditions:

```go
func Signum(x int) int {
    switch {
    case x > 0:
        return +1
    default:
        return 0
    case x < 0:
        return -1
    }
}
```

## Key Points

- Cases evaluated top to bottom
- Default case is optional but recommended
- Switch doesn't need an operand (tagless switch)

## Control Flow

- `break` → go to next statement after switch
- No automatic fallthrough (unlike C)

## Where I Learned This

- [[1.8 Loose Ends]]

## Related Concepts

- [[Control Flow]]
- [[If Statements]]