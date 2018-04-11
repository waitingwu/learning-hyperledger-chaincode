# Variables 變數

變數可以連續宣告，並依序給初始值

```go
var i, j int = 1, 2
```

## Short variable declarations

在函式中，可以用 := 來取代 var 做為變數宣告，函式外則必須使用關鍵字做為開頭\(var, func 等等\)，故 := 在函式外不可用

```go
package main

import "fmt"

func main() {
    var i, j int = 1, 2
    k := 3
    c, python, java := true, false, "no!"

    fmt.Println(i, j, k, c, python, java)
}
```

## Zero values

沒有給定初始值的變數，Go 會指派 zero value 給它：

```go
package main

import "fmt"

func main() {
    var i int
    var f float64
    var b bool
    var s string
    fmt.Printf("%v %v %v %q\n", i, f, b, s) //0 0 false ""
}
```

註：常數\(const\)宣告不能用 := 語法



## Type conversions

T\(v\) 表示式將 v 轉為 type T，例：

```
var i int = 42
var f float64 = float64(i)
var u uint = uint(f)
```

或是可以簡化為：

```
i := 42
f := float64(i)
u := uint(f)
```



## Numeric Constants

數值常數具有高精準度

```go
package main

import "fmt"

const (
	// Create a huge number by shifting a 1 bit left 100 places.
	// In other words, the binary number that is 1 followed by 100 zeroes.
	Big = 1 << 100
	// Shift it right again 99 places, so we end up with 1<<1, or 2.
	Small = Big >> 99
)

func needInt(x int) int { return x*10 + 1 }
func needFloat(x float64) float64 {
	return x * 0.1
}

func main() {
	fmt.Println(needInt(Small)) 	// 21
	fmt.Println(needInt(Big)) 	// 會overflow
	fmt.Println(needFloat(Small)) 	// 0.2
	fmt.Println(needFloat(Big)) 	// 1.2676506002282295e+29
}
```



