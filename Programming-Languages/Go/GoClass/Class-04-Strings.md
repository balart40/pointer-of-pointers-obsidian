---
tags:
  - Go
  - Golang
---
## Strings

An immutable sequence of "characters" 
- physically a sequence of bytes (UTF-8 encoding)
- logically a sequence of (unicode) runes
### Runes 
Are encoded in single quotes 'a'

"Raw" strings use backtick quotes 
They also don't evaluate escape characters such as `\n `

```
package main

import (
	"fmt"
)

func main() {

	s := "elite"
	
	fmt.Printf("%8T %[1]v %d\n", s, len(s))
	fmt.Printf("%8T %[1]v\n", []rune(s))

	b := []byte(s)
	fmt.Printf("%8T %[1]v %d\n", b, len(b))
}
```