---
tags:
  - Go
  - Golang
---
``` 
package main

import (
	"fmt"
	"os"
)

func main() {
	fmt.Printf("Hello, %s\n", os.Args[1])
}
```

New hello world taking parameters

```
package main

import (
	"fmt"
	"os"
)

func main() {
	if len(os.Args) > 1 {
		fmt.Printf("Hello, %s\n", os.Args[1])
	} else {
		fmt.Println("Hello world")
	}
}
```

Significant changes since the book

Language
1. for range with no variable (1.4)
2. internal packages with limited visibility (1.5)
3. struct conversion with mismatched tags (1.8)
4. type aliases (1.9)
5. Go modules (1.11+)
6. improved numeric literals and error handling (1.13)
7. overlapping interfaces (1.4)

Runtime
1. Performance improvements in every release
2. full (async) preemption of goroutines (1.14)

