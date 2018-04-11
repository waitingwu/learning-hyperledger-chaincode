# Package

每隻 Go 程式都是由 packages 組成

根據 Go 的開發規範，package name 跟 import path 的最後一個元素相同，例如：

```go
"math/rand"
```

該 import file 的 package 就是

```go
package rand
```

## Imports

Import可以長這樣：

```go
import "fmt"
import "math"
```

也可以長這樣：

```go
import (
    "fmt"
    "math"
)
```

上述方式稱為 "factored" import statement，比較常用

## Exported names

在 Go 語言裡，要給外部\(自己的 package 以外\)使用的變數名稱都要大寫開頭，像是 Pi ，任何非大寫開頭的變數視為 unexported，外部就無法 access，如 pi

```go
package main

import (
    "fmt"
    "math"
)

func main() {
    fmt.Println(math.Pi)
}
```



