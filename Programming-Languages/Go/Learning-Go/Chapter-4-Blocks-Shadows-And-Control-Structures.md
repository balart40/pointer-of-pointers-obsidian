---
tags:
  - Go
  - Golang
  - Programming-Language
---
## Blocks

Can be declared outside of functions, as the parameter to functions, and as local variables within functions

Each place where a declaration occurs is called a block. 

Variables, constants, types, and functions declared outside of ay functions are placed in the **package block**.

The names for other packages that are valid for the file that contains the import statements are in the **file block**.

When you have a declaration with the same name as an identifier in a containing block, it is said that you **shadow the identifier** created in the outer block.

### Shadowing Variables

```
func main() {
    x := 10
    if x > 5 {
        fmt.Println(x)
        x := 5
        fmt.Println(x)
    }
    fmt.Println(

```

This will print 

```
10
5
10
```

A shadowing variable is a variable that has the same name as a variable in a containing block. For as long as the shadowing variable exists, you cannot access a shadowed variable.

Below you will found an example of shadowing with multiple assignment

```
func main() {
    x := 10
    if x > 5 {
        x, y := 5, 20
        fmt.Println(x, y)
    }
    fmt.Println(x)
} Running

```

Which will print

```
5, 20
10
```

Although there was an existing definition of x in an outer block, x was still shadowed within the if statement. That’s because := only reuses variables that are declared in the current block. When using :=, make sure that you don’t have any variables from an outer scope on the lefthand side, unless you intend to shadow them.

### Detecting Shadowed Variables

You can add shadowing detection to your build process by installing the shadow linter on your machine

```
go install golang.org/x/tools/go/analysis/passes/shadow/cmd/shadow@latest
```

If you are building with a Makefile, consider including shadow in the vet task: 

```
vet:
	go vet ./...
    shadow
.PHONY:vet
```
And you will se what variables are detected to have shadowing with a similar message as shown below

```
declaration of "x" shadows declaration at line 6
```

The built-in types like `int`, `string`, `true`, `false`, and functions like `make` or `close` are not included in the 25 keywords of Go, they are considered as predeclared identifiers and are defined in the universe block.

This means that these names can be shadowed in other scopes
You must be very careful to never redefine any of the identifiers in the universe block.

## If

An `If` example below

```
n := rand.Intn(10)
if n == 0 {
	fmt.Println("That's too low")
} else if n > 5 {
    fmt.Println("That's too big:", n)
} else {
    fmt.Println("That's a good number:", n)
}
```

Go allows to have variables only scoped within the if else clauses

```
if n := rand.Intn(10); n == 0 {
    fmt.Println("That's too low")
} else if n > 5 {
    fmt.Println("That's too big:", n)
} else {
    fmt.Println("That's a good number:", n)
} 
```



```
if n := rand.Intn(10); n == 0 {
    fmt.Println("That's too low")
} else if n > 5 {
	fmt.Println("That's too big:", n)
} else {
    fmt.Println("That's a good number:", n)
}
fmt.Println(n) 
```

This will print `undefined: n` since the hardcoded random will throw 1

## For, four ways

- A complete, C-style for
- A condition-only for
- An infinite for
- for-range

### The complete for statement

Example shown below

```
for i := 0; i < 10; i++ {
    fmt.Println(i)
}
```

- First, you must use := to initialize the variables; var is not legal here. 
- Second, just like variable declarations in if statements, you can shadow a variable here.
### The condition-Only for statement

Go allows you to leave off both the initialization and the increment in a for statement.

```
i := 1
for i < 100 {
        fmt.Println(i)
        i = i * 2
}
```

### The infinite for statement

```
package main

import "fmt"

func main() {
    for {
        fmt.Println("Hello")
    }
}
```

### Break and continue

The equivalent of a do while loop of java such as the one one shown below

```
do {
    // things to do in the loop
} while (CONDITION);
```

I go would be
```
 for {
    // things to do in the loop
    if !CONDITION {
        break
    }
}
```

Although Go has the `continue` keyword to skip the rest of the body of a for loop you dont need it

```
for i := 1; i <= 100; i++ {
    if i%3 == 0 {
        if i%5 == 0 {
            fmt.Println("FizzBuzz")
        } else {
            fmt.Println("Fizz")
        }
	} else if i%5 == 0 {
        fmt.Println("Buzz")
    } else {
        fmt.Println(i)
    }
}
```

But this is not idiomatic. Go encourages short if statement bodies, as left-aligned as possible.

```
for i := 1; i <= 100; i++ {
    if i%3 == 0 && i%5 == 0 {
        fmt.Println("FizzBuzz")
        continue
    }
    if i%3 == 0 {
        fmt.Println("Fizz")
        continue
    }
    if i%5 == 0 {
        fmt.Println("Buzz")
        continue
    }
    fmt.Println(i)
} 
```

### The for range statement

You can only use a for-range loop to iterate over the built-in compound types and user-defined types that are based on them.

```
evenVals := []int{2, 4, 6, 8, 10, 12}
for i, v := range evenVals {
    fmt.Println(i, v)
} 
```

will output

```
0 2
1 4
2 6
3 8
4 10
5 12
```

Go requires you to access all declared variables, if you don´t need it you can use `_`

```
evenVals := []int{2, 4, 6, 8, 10, 12}
for _, v := range evenVals {
    fmt.Println(v)
}
```

What if you want the key, but don’t want the value? In this situation, Go allows you to just leave off the second variable.

```
uniqueNames := map[string]bool{"Fred": true, "Raul": true, "Wilma": true}
for k := range uniqueNames {
    fmt.Println(k)
}
```

### Iterating over maps

```
m := map[string]int{
    "a": 1,
    "c": 3,
    "b": 2,
}

for i := 0; i < 3; i++ {
    fmt.Println("Loop", i)
    for k, v := range m {
        fmt.Println(k, v)
    }
}
```

### Iterating over string

```
func main() {
	samples := []string{"hello", "apple_π!"}
for _, sample := range samples {
    for i, r := range sample {
        fmt.Println(i, r, string(r))
    }
    fmt.Println()
}
```

Would print 

```
0 104 h
1 101 e
2 108 l
3 108 l
4 111 o

0 97 a
1 112 p
2 112 p
3 108 l
4 101 e
5 95 _
6 960 π
8 33 !

```
### The for-range is a copy

You should be aware that each time the for-range loop iterates over your compound type, it copies the value from the compound type to the value variable.

```
evenVals := []int{2, 4, 6, 8, 10, 12}
for _, v := range evenVals {
    v *= 2
}
fmt.Println(evenVals)
```
which would output

```
[2 4 6 8 10 12]
```

### Labeling your for statements

```
func main() {
    samples := []string{"hello", "apple_π!"}
outer:
    for _, sample := range samples {
        for i, r := range sample {
            fmt.Println(i, r, string(r))
            if r == 'l' {
                continue outer
            }
        }
        fmt.Println()
    }
} 
```

Would output

```
0 104 h
1 101 e
2 108 l
0 97 a
1 112 p
2 112 p
3 108 l
```

### Choosing the right for statement

Favor a for-range loop when iterating over all the contents of an instance of one of the built-in compound types.

```
evenVals := []int{2, 4, 6, 8, 10}
for i, v := range evenVals {
    if i == 0 {
        continue
    }
    if i == len(evenVals)-1 {
        break
    }
    fmt.Println(i, v)
}
```

also we have

```
evenVals := []int{2, 4, 6, 8, 10}
for i := 1; i < len(evenVals)-1; i++ {
	fmt.Println(i, evenVals[i])
}
```

## Switch

- You don't put parenthesis around the value being compared in a switch
- Also like an `if` statement you can declare a variable that's scoped to all branches like in the example below `size`
- You don't put braces around the contents of the case clauses
- You can have multiple lines inside a case clause
- You don't need to put a break at the end of the case
- You separate  multiple matches with commas
- case. However, the need for a break statement might indicate that you are doing something too complicated.

```
words := []string{"a", "cow", "smile", "gopher",
    "octopus", "anthropologist"}
for _, word := range words {
    switch size := len(word); size {
    case 1, 2, 3, 4:
        fmt.Println(word, "is a short word!")
    case 5:
        wordLen := len(word)
        fmt.Println(word, "is exactly the right length:", wordLen)
    case 6, 7, 8, 9:
    default:
        fmt.Println(word, "is a long word!")
    }
}
```

Below is the example of a switch with a break inside a for loop
```
func main() {
    for i := 0; i < 10; i++ {
        switch {
        case i%2 == 0:
            fmt.Println(i, "is even")
        case i%3 == 0:
            fmt.Println(i, "is divisible by 3 but not 2")
        case i%7 == 0:
            fmt.Println("exit the loop!")
            break
        default:
            fmt.Println(i, "is boring")
        }
    }
}
```

### Blank switches

You can write a switch statement that doesn’t specify the value that you’re comparing against. This is called a **blank switch**.

A regular switch only allows you to check a value for equality. A blank switch allows you to use any boolean comparison for each case.

```
words := []string{"hi", "salutations", "hello"}
for _, word := range words {
    switch wordLen := len(word); {
    case wordLen < 5:
        fmt.Println(word, "is a short word!")
    case wordLen > 10:
        fmt.Println(word, "is a long word!")
	default:
        fmt.Println(word, "is exactly the right length.")
    }
}
```

Just like a regular switch statement, you can optionally include a short variable declaration as part of your blank switch. 

If you find that you have written a blank switch where all of your cases are equality comparisons against the same variable:

```
switch {
case a == 2:
    fmt.Println("a is 2")
case a == 3:
    fmt.Println("a is 3")
case a == 4:
    fmt.Println("a is 4")
default:
    fmt.Println("a is ", a)
}
```

you should replace it with an expression switch statement:

```
switch a {
case 2:
    fmt.Println("a is 2")
case 3:
    fmt.Println("a is 3")
case 4:
    fmt.Println("a is 4")
default:
    fmt.Println("a is ", a)
}
```

## Choosing between if and switch

Favor blank switch statements over if/else chains when you have multiple related cases. Using a switch makes the comparisons more visible and reinforces that they are a related set of concerns.

## Goto

don't use goto ...