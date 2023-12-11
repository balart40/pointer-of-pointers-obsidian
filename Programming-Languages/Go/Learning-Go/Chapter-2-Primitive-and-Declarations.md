---
tags:
  - Go
  - Programming-Language
---
## Built-in Types

Go has the same built-in types as other languages:
- booleans
- integers
- floats
- strings
### The Zero Value

Go, will assign a default zero value to any variable that is declared but not assigned value.
## Literals

There are four common kinds of literals on Go (rare 5th)

***Integer Literals***
Are sequence of numbers, depending on the prefix, will be the base
- 0b (base two) - Binary
- 0o (base eight) - Octal
- 0x (base sixteen) - Hexadecimal

Additionally, for longer literals, you can use underscores for example
```
1234
```
Can be written
```
1_234
```

***Floating point Literals***

Used to indicate the fractional portion of the value. Also, support exponent specified as well as positive and negative numbers.
```
6.03e23
```

***Rune Literals***

Represent characters surrounded by single quotes.
Unlike other languages, in Go, **single quotes and double quotes are not interchangeable**. Examples are shown below

| Description              | Example |
| :---------------- | :------: | 
| Single Unicode characters    | `'a'`   | 
| 8-bit octal numbers| `'\141'` |
| 8-bit hexadecimal numbers `'\x61'` |
| 16-bit hexadecimal numbers| `'\u0061'` |
| 32-bit Unicode numbers| `'\U00000061` |
| new line| `'\n'` |
| tab| `'\t'` |
| single quote| `'\''` |
| double quote| `'\""` |
| backslash| `'\\` |
### Strings

***Interpreted string literals***

- You should use double quotes to create an interpreted string literal.
- These contain zero or more rune literals
- The only characters that cannot appear are unescaped backslashes, newlines and double quotes.
- For example, new line with Salutations in quotes ("Salutations") would like as
```
"Greetings and\n\"Salutations\"".
```

***Raw string literals***
- If you need to include backslashes , double quotes, or new lines in your string use raw string literal.
- These are delimited with backquotes 
```
`Greeting and 
"Salutations"`
```

**Literals in Go are untyped; they can interact with any variable that's compatible with the literal**

When the type isn't explicitly declared, Go, will use the ***default type* for a literal
### Booleans

The `bool` type represents boolean variables, with two values : `true` or `false` when not assigned default is `false`.

```
var flag bool // false
var isAwesome = true
```

### Numeric types
Go has 12 different types of numeric types, grouped in three types: ***Integer types*, *special integer types*, *uint***

***Integer Types***
Provides both signed and unsigned integers from one to eight bytes

| Description              | Example |
| :---------------- | :------: | 
| int8  | -128 to 127   | 
| int16  | –32768 to 32767   | 
| int32  | –2147483648 to 2147483647   | 
| int64  | –9223372036854775808 to 9223372036854775807    | 
| uint8  | 0 to 255   | 
| uint16  | 0 to 65535   | 
| uint32  | 0 to 4294967295   | 
| uint64  | 0 to 18446744073709551615| 

***Special Integer Types***

byte = utin8
int in 32 CPU is an int32 or int64 for 64 CPU

Integer literals default to being of int type

***uint***
Unsigned Integer
### Integer operators

- +
- -
- *
- /
- % for modulus

```
var x int = 10
x *= 2
```

You can compare integers with
- ==
- !=
- >=
- <=

You can do bit-manipulation such as:
- Shift left: <<
- Shift right: >>
Or do bit masks with 
- & (Logical AND)
- | (Logical OR)
- ^ (LOCICAL XROR)
- &^ (LOGICAL AND NOT)

Just like the arithmetic operators, you can also combine all of the logical operators with = to modify a variable: 

```
&=, |=, ^=, &^=, <<=, and >>=.

```

***Floating Point Types***

| Description              | Largest abs val | Smalles (nonzero)|abs val |
|- |- |-  |
| float32  | 3.40282346638528859811704183484516925440e+38    |  1.401298464324817070923729583289916131280e-45 
| float64  | 1.797693134862315708145274237317043567981e+308     |  4.940656458412465441765687928682213723651e-324 |

Dividing a nonzero floating point variable by 0 returns +Inf or -Inf
dividing a floating point variable set to 0 by 0 return Nan (Not a Number)

***Complex Types***

Go defines
- complex64 to use float32 values to represent the real and imaginary part
- complex128 uses float64 values
- Default is complex128

For example:

```
package main

import (
	"fmt"
	"math/cmplx"
)

func main() {
	x := complex(2.5, 3.1)
	y := complex(10.2, 2)
	fmt.Println(x + y)
	fmt.Println(x - y)
	fmt.Println(x * y)
	fmt.Println(x / y)
	fmt.Println(real(x))
	fmt.Println(imag(x))
	fmt.Println(cmplx.Abs(x))
}
```

when run gives:

```
(12.7+5.1i)
(-7.699999999999999+1.1i)
(19.3+36.62i)
(0.2934098482043688+0.24639022584228065i)
2.5
3.1
3.982461550347975
```
##  A taste of string and runes

- The zero value for a string is the empty string
- String in Go are immutable, you can reassign the value of a string variable but you cannot change the value of the string that is assigned to it
- The rune type is an alias for the int32 type.
## Explicit type conversion

- Go doesn't allow automatic type promotion between variables, event different size variables need to be converted as shown below
```
	var x int = 10
	var y float64 = 30.2
	var z float64 = float64(x) + y
	var d int = x + int(y)
	fmt.Println(z, d)
```

Gives
```
40.2 40
```
## Var versus :=

Each declaration style in Go communicates something about how the variable is used.
The most verbose way is using the `var`  keyword, and the explicit type and an assignment

```
var x int  = 10
```

If the type on the righthand side of the  = is the expected type you can leave off the type from the left side

```
var x = 10
```

If you want to leave the default value zero you can just

```
var x int
```

Below a different types:

```
var x, y = 10, "hello"
```

If you are declaring multiple variables at once, you can wrap them in a declaration list: 

```
var (
    x    int
    y        = 20
    z    int = 30
    d, e     = 40, "hello"
    f, g string
)
```

For short declaration format we use `:=` that uses type inference

```
var x  = 10
x := 10
```

Similarly you can do multiple variable declaration

```
x, y := 10, "hello"
```

The := operator can do one trick that you cannot do with var: it allows you to assign values to existing variables, too.

There is one limitation on :=. If you are declaring a variable at package level, you must use var because := is not legal outside of functions.

While it is legal to use a type conversion to specify the type of the value and use := to write

```
x := byte(20)
```

it is idiomatic to write 
```
var x byte = 20.
```
While var and := allow you to declare multiple variables on the same line, only use this style when assigning multiple values returned from a function or the comma ok idiom

As a general rule, you should only declare variables in the package block that are effectively immutable.

Avoid declaring variables outside of functions because they complicate data flow analysis.
### Using const

Constants in Go are a way to give names to literals. They can only hold values that the compiler can figure out at compile time. This means that they can be assigned: 
- Numeric literals 
- true and false 
- Strings 
- Runes 
- The built-in functions complex, real, imag, len, and cap 
- Expressions that consist of operators and the preceding values

Go doesn’t provide a way to specify that a value calculated at runtime is immutable. 

There are no immutable arrays, slices, maps, or structs, and there’s no way to declare that a field in a struct is immutable.

Constants in Go are a way to give names to literals. There is no way in Go to declare that a variable is immutable.
#### Typed and Untyped Constants 

Constants can be typed or untyped. An untyped constant works exactly like a literal; it has no type of its own, but does have a default type that is used when no other type can be inferred.

Therefore if we have 
```
const x =  10
```
The following are legal
```
var y int = x
var z float64 = x
var d byte = x
```
## Unused variables

Another Go requirement is that every declared local variable must be read. It is a compile-time error to declare a local variable and to not read its value.

