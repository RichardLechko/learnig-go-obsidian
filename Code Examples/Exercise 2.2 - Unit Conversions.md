## Chapter

[[2.6 Packages and Files]]

## Task

Write a general-purpose unit-conversion program analogous to `cf` that reads numbers from its command-line arguments or from the standard input if there are no arguments, and converts each number into units like temperature in Celsius and Fahrenheit, length in feet and meters, weight in pounds and kilograms, and the like.

## Project Structure

```bash
.
├── conversions
│   ├── go.mod
│   ├── lengthconv
│   │   ├── conv.go
│   │   └── lengthconv.go
│   └── main.go
└── excercise-explanation.txt
```

## File: `conversions/go.mod`

```go
module conversions

go 1.22.2
```

Created with: `go mod init conversions`

## File: `conversions/lengthconv/lengthconv.go`

```go
// Package lengthconv performs length conversions using the metric system
package lengthconversions

import "fmt"

type Millimeter float64
type Centimeter float64
type Meter      float64
type Kilometer  float64

func (mm Millimeter) String() string {
    return fmt.Sprintf("%gmm", mm)
}

func (cm Centimeter) String() string {
    return fmt.Sprintf("%gcm", cm)
}

func (m Meter) String() string {
    return fmt.Sprintf("%gm", m)
}

func (km Kilometer) String() string {
    return fmt.Sprintf("%gkm", km)
}
```

## File: `conversions/lengthconv/conv.go`

```go
package lengthconversions

// Millimeters to Centimeters
func MMToCM(mm Millimeter) Centimeter {
    return Centimeter(mm / 10)
}

// Millimeters to Meters
func MMToM(mm Millimeter) Meter {
    return Meter(MMToCM(mm) / 100)
}

// Millimeters to Kilometers
func MMToKM(mm Millimeter) Kilometer {
    return Kilometer(MMToM(mm) / 1000)
}

// Centimeters to Millimeters
func CMToMM(cm Centimeter) Millimeter {
    return Millimeter(cm * 10)
}

// Centimeters to Meters
func CMToM(cm Centimeter) Meter {
    return Meter(cm / 100)
}

// Centimeters to Kilometers
func CMToKM(cm Centimeter) Kilometer {
    return Kilometer(CMToM(cm) / 1000)
}

// Meters to Millimeters
func MToMM(m Meter) Millimeter {
    return Millimeter(MToCM(m) * 10)
}

// Meters to Centimeters
func MToCM(m Meter) Centimeter {
    return Centimeter(m * 100)
}

// Meters to Kilometers
func MToKM(m Meter) Kilometer {
    return Kilometer(m / 1000)
}

// Kilometers to Millimeters
func KMToMM(km Kilometer) Millimeter {
    return Millimeter(KMToCM(km) * 10)
}

// Kilometers to Centimeters
func KMToCM(km Kilometer) Centimeter {
    return Centimeter(KMToM(km) * 100)
}

// Kilometers to Meters
func KMToM(km Kilometer) Meter {
    return Meter(km * 1000)
}
```

## File: `conversions/main.go`

```go
package main

import (
    "fmt"
    "os"
    "strconv"
    "conversions/lengthconv"
)

func main() {
    for _, arg := range os.Args[1:] {
        t, err := strconv.ParseFloat(arg, 64)
        if err != nil {
            fmt.Fprintf(os.Stderr, "cf: %v\n", err)
            os.Exit(1)
        }
        
        mm := lengthconversions.Millimeter(t)
        cm := lengthconversions.Centimeter(t)
        m  := lengthconversions.Meter(t)
        km := lengthconversions.Kilometer(t)
        
        fmt.Println("KILOMETER CONVERSION")
        fmt.Println("=================================================")
        fmt.Printf("KM: %s \t M: %s\n", km, lengthconversions.KMToM(km))
        fmt.Printf("KM: %s \t CM: %s\n", km, lengthconversions.KMToCM(km))
        fmt.Printf("KM: %s \t MM: %s\n", km, lengthconversions.KMToMM(km))
        fmt.Printf("=================================================\n\n")
        
        fmt.Println("METER CONVERSION")
        fmt.Println("=================================================")
        fmt.Printf("M: %s \t KM: %s\n", m, lengthconversions.MToKM(m))
        fmt.Printf("M: %s \t CM: %s\n", m, lengthconversions.MToCM(m))
        fmt.Printf("M: %s \t MM: %s\n", m, lengthconversions.MToMM(m))
        fmt.Printf("=================================================\n\n")
        
        fmt.Println("CENTIMETER CONVERSION")
        fmt.Println("=================================================")
        fmt.Printf("CM: %s \t KM: %s\n", cm, lengthconversions.CMToKM(cm))
        fmt.Printf("CM: %s \t M: %s\n", cm, lengthconversions.CMToM(cm))
        fmt.Printf("CM: %s \t MM: %s\n", cm, lengthconversions.CMToMM(cm))
        fmt.Printf("=================================================\n\n")
        
        fmt.Println("MILLIMETER CONVERSION")
        fmt.Println("=================================================")
        fmt.Printf("MM: %s \t KM: %s\n", mm, lengthconversions.MMToKM(mm))
        fmt.Printf("MM: %s \t M: %s\n", mm, lengthconversions.MMToM(mm))
        fmt.Printf("MM: %s \t CM: %s\n", mm, lengthconversions.MMToCM(mm))
        fmt.Printf("=================================================\n\n")
    }
}
```

## How to Run

```bash
cd conversions
go build main.go
./main 5
```

## Output Example

```txt
KILOMETER CONVERSION
=================================================
KM: 5km          M: 5000m
KM: 5km          CM: 500000cm
KM: 5km          MM: 5e+06mm
=================================================

METER CONVERSION
=================================================
M: 5m    KM: 0.005km
M: 5m    CM: 500cm
M: 5m    MM: 5000mm
=================================================

CENTIMETER CONVERSION
=================================================
CM: 5cm          KM: 5e-05km
CM: 5cm          M: 0.05m
CM: 5cm          MM: 50mm
=================================================

MILLIMETER CONVERSION
=================================================
MM: 5mm          KM: 5e-06km
MM: 5mm          M: 0.005m
MM: 5mm          CM: 0.5cm
=================================================
```

## Concepts Used

- [[Packages]] - creating custom package
- [[Modules]] - using go.mod
- [[Named Types]] - Millimeter, Centimeter, Meter, Kilometer
- [[Methods]] - String() methods for each type
- [[Type Conversions]] - converting between length units
- [[Package-Level Declarations]] - types are package-level
- [[Import Paths]] - importing custom package

## Key Learnings

1. How to organize code into packages
2. How to create a module with go.mod
3. How to import and use custom packages
4. How named types provide type safety for units