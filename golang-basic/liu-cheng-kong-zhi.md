# 流程控制

Go 的 for, if 等等，條件都不需用\(\)包住

## for loop

for 迴圈可以這樣寫：

```go
for i := 0; i < 10; i++ {
    sum += i
}
```

也可以這樣寫：

```go
for ; sum < 1000; {
    sum += sum
}
```

## For is Go's "while"

\(把前一個例子的for loop兩個分號拿掉之後\)，Go 的 for loop 就是 while：

```go
for sum < 1000 {
    sum += sum
}
```

## 無窮迴圈

```go
for {
    ......
}
```

## If with a short statement

if 沒啥特別的，但可以在執行條件判斷前做別的事：

```go
package main

import (
    "fmt"
    "math"
)

func pow(x, n, lim float64) float64 {
    if v := math.Pow(x, n); v < lim {
        return v
    } else {
        fmt.Printf("%g >= %g\n", v, lim)
    }
    // can't use v here, though
    return lim
}

func main() {
    fmt.Println(
        pow(3, 2, 10),
        pow(3, 3, 20),
    )
}
```

## Switch

Go 的 switch 和其他語言差不多，除了幾點：

* Go 的 switch 在執行某個 case 之後就會自動 break
* Go 的 switch case 不必為常數
* Go 的 switch value 不必為整數

```go
package main

import (
    "fmt"
    "runtime"
)

func main() {
    fmt.Print("Go runs on ")
    switch os := runtime.GOOS; os {
    case "darwin":
        fmt.Println("OS X.")
    case "linux":
        fmt.Println("Linux.")
    default:
        // freebsd, openbsd,
        // plan9, windows...
        fmt.Printf("%s.", os)
    }
}
```

其它的 switch 例子：

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    fmt.Println("When's Saturday?")
    today := time.Now().Weekday()
    switch time.Saturday {
    case today + 0:
        fmt.Println("Today.")
    case today + 1:
        fmt.Println("Tomorrow.")
    case today + 2:
        fmt.Println("In two days.")
    default:
        fmt.Println("Too far away.")
    }
}
```

沒有條件的 switch：

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	t := time.Now()
	switch {
	case t.Hour() < 12:
		fmt.Println("Good morning!")
	case t.Hour() < 17:
		fmt.Println("Good afternoon.")
	default:
		fmt.Println("Good evening.")
	}
}
```

## Defer

Defer 會將該函式延緩到周圍函式都 return 了才執行，旦 deferred call 的參數會立刻被計算

```go
package main

import "fmt"

func main() {
	defer fmt.Println("world")

	fmt.Println("hello")
}
// hello
// world
```

## Stacking defers

Deferred function calls 會被放到 stack，執行時會採 last-in-first-out 的順序

```go
package main

import "fmt"

func main() {
	fmt.Println("counting")

	for i := 0; i < 10; i++ {
		defer fmt.Println(i)
	}

	fmt.Println("done")
}

// counting
// done
// 9
// 8
// 7
// 6
// 5
// 4
// 3
// 2
// 1
// 0
```



