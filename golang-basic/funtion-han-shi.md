# func 函式

Go 函式的參數形態可以這樣給：

```go
func add(x int, y int) int {
	return x + y
}
```

也可以這樣給：

```go
func add(x, y int) int {
	return x + y
}
```



Go 函式允許多個傳回值，如下例的 \(string, string\)：

```go
package main

import "fmt"

func swap(x, y string) (string, string) {
	return y, x
}

func main() {
	a, b := swap("hello", "world")
	fmt.Println(a, b)
}
```

傳回多值時，指定給變數時必須依順序，若不需要某個傳回值，可以使用`_`略過：

```go
_, name := FirstMatch(names, "Huang")
```



官方建議要宣告傳回值名稱，Ex：gcd

```go
func Gcd(m, n int) (gcd int) {
    ......
    gcd = 5
    ......
    return
}
```

#### 

#### Receiver

Go 沒有class，但可以為type定義method，達成類似效果，如：

```go
package main

import (
    "fmt"
    "math"
)

type Vertex struct {
    X, Y float64
}

func (v Vertex) Abs() float64 {
    return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

func main() {
    v := Vertex{3, 4}
    fmt.Println(v.Abs())
}
```

上述例子，Abs\(\) 有一個type為Vertex、名為v的receiver，main\(\)在呼叫時就可以透過Vertex的instance v，直接呼叫Abs\(\)

> 注意：method 只是一個具有 receiver argument 的 function

```go
package main

import (
    "fmt"
    "math"
)

type Vertex struct {
    X, Y float64
}

func Abs(v Vertex) float64 {
    return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

func main() {
    v := Vertex{3, 4}
    fmt.Println(Abs(v))
}
```

> 注意：method的receiver的type必須和method在同一個package

#### Pointer receivers

使用Pointer receivers的methods可以改變receiver所指到的值，實務上常用到

```go
package main

import (
    "fmt"
    "math"
)

type Vertex struct {
    X, Y float64
}

func (v Vertex) Abs() float64 {
    return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

func (v *Vertex) Scale(f float64) {
    v.X = v.X * f
    v.Y = v.Y * f
}

func main() {
    v := Vertex{3, 4}
    v.Scale(10)
    fmt.Println(v.Abs()) //return 50
}
```



