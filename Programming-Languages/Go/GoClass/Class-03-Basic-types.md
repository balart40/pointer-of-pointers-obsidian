---
tags:
  - Golang
  - Go
---
### Machine-native vs interpreted

a = 2
#### In interpreter

A is an object that represents or masquerades as a number in the interpreter
#### Go

a is purely the name or address of a memory location in the machine
- No JVM
- No abstraction
##### Int 

Int is the default type for integers in Go, even lengths

##### Floating point numbers

float32 float64

### Simple Declarations

Anywhere

```
var a int
```

or

```
car (
	b = 2
	f = 2.01
)
```

Only inside functions:

```
c := 2
```

An example

```
package main

import "fmt"

func main() {
	a := 2
	b := 3.1
	fmt.Printf("a: %8T %v\n", a, a)
	fmt.Printf("b: %8T %[1]v\n", b)

	a = int(b)
	fmt.Printf("a: %8T %[1]v\n", a)
	b = float64(a)
	fmt.Printf("b: %8T %[1]v\n", b)
}
```

### Simple types

#### Special types

##### bool (boolean) 

George boole

has two values false, true
these values are not convertible to/from integers!
##### error

A special type with one function, Error()
an error may be nil or non-nil

Pointers are physically addresses, logically opaque

a pointer may be nil or non-nil
no pointer manipulation except through package unsafe

#### Initialization

Go initializes all variables to "zero" by default if you don't
- All numerical types get 0
- bool gets false
- strings gets ""
- Everything else gets nil
	- Pointers
	- slices
	- maps
	- channels
	- functions (function variables)
	- interfaces

For aggregate types all members get their "zero" values

#### Constants

Means immutable

Only numbers, strings, and booleans can be constants (immutable)

constant can be a literal or a compile-time function of a constant

