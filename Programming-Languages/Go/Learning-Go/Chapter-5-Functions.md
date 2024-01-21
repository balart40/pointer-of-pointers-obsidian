---
tags:
  - Go
  - Golang
  - Programming-Language
---
## Declaring and Calling Functions

### Declaring and calling functions

The following example shows a function that return a value

```
func div(numerator int, denominator int) int {
    if denominator == 0 {
        return 0
    }
    return numerator / denominator
}
```

A function declaration consists in four parts:
- The keyword `func`
- the name of the function
- the input parameters 
- the return type

When a function returns nothing, you write nothing between the input parameter’s closing parenthesis and the opening brace for the function body:

```
func main() {
    result := div(5, 2)
    fmt.Println(result)
} Calling a function should be familiar
```

When you have multiple input parameters of the same type, you can write your input parameters like this:

```
func div(numerator, denominator int) int {
```

### Simulating Named and Optional Parameters

If you want to emulate named and optional parameters, define a struct that has fields that match the desired parameters, and pass the struct to your function.

```
type MyFuncOpts struct {
    FirstName string
    LastName string
    Age int
}

func MyFunc(opts MyFuncOpts) error {
    // do something here
}

func main() {
    MyFunc(MyFuncOpts {
        LastName: "Patel",
        Age: 50,
    })
    My Func(MyFuncOpts {
        FirstName: "Joe",
        LastName: "Smith",
    })
}
```

### Variadic Input Parameters and Slices

Go supports variadic parameters. The variadic parameter must be the last (or only) parameter in the input parameter list. You indicate it with three dots (…) before the type.

```
func addTo(base int, vals ...int) []int {
    out := make([]int, 0, len(vals))
    for _, v := range vals {
		out = append(out, base + v)
    }
    return out
}
```

And now we can call it in several ways

```
func main() {
    fmt.Println(addTo(3))
    fmt.Println(addTo(3, 2))
    fmt.Println(addTo(3, 2, 4, 6, 8))
    a := []int{4, 3}
    fmt.Println(addTo(3, a...))
    fmt.Println(addTo(3, []int{1, 2, 3, 4, 5}...))
}
```

```
func main() {
    fmt.Println(addTo(3))
    fmt.Println(addTo(3, 2))
    fmt.Println(addTo(3, 2, 4, 6, 8))
    a := []int{4, 3}
    fmt.Println(addTo(3, a...))
    fmt.Println(addTo(3, []int{1, 2, 3, 4, 5}...))
}
```

The output would be

```
[]
[5]
[5 7 9 11]
[7 6]
[4 5 6 7 8]
```

### Multiple Return Values

When there are multiple return variables they are listed in parentheses after the function arguments as you can see below

Also, you must return all the multiple values separated by commas

```
func divAndRemainder(numerator int, denominator int) (int, int, error) {
    if denominator == 0 {
        return 0, 0, errors.New("cannot divide by zero")
    }
    return numerator / denominator, numerator % denominator, nil
}
```

If the function completes successfully, we return `nil` for the error’s value. By convention, the error is always the last (or only) value returned from a function.

```
func main() {
    result, remainder, err := divAndRemainder(5, 2)
    if err != nil {
        fmt.Println(err)
        os.Exit(1)
    }
    fmt.Println(result, remainder)
}
```

### Multiple Return Values Are Multiple Values

You must assign each value returned from a function. If you try to assign multiple return values to one variable, you get a compile-time error.

### Ignoring Returned Values

You cannot have unused variables in go, if you don't use it you can just assign it to `_`
### Named Return Values

In addition to letting you return more than one value from a function, Go also allows you to specify names for your return values.

```
func divAndRemainder(numerator int, denominator int) (result int, remainder int,
                                                                  err error) {
    if denominator == 0 {
        err = errors.New("cannot divide by zero")
        return result, remainder, err
    }
    result, remainder = numerator/denominator, numerator%denominator
    return result, remainder, err
}
```

One important thing to note: the name that’s used for a named returned value is local to the function; it doesn’t enforce any name outside of the function. It is perfectly legal to assign the return values to variables of different names: 

```
func main() {
    x, y, z := divAndRemainder(5, 2)
    fmt.Println(x, y, z)
}
```

Be careful since once the variables are defined as return, they can be shadowed

```
func divAndRemainder(numerator, denominator int) (result int, remainder int,
                                                              err error) {
    // assign some values
    result, remainder = 20, 30
    if denominator == 0 {
        return 0, 0, errors.New("cannot divide by zero")
    }
    return numerator / denominator, numerator % denominator, nil
}
```

The values from the return statement were returned even though they were never assigned to the named return parameters. That’s because the Go compiler inserts code that assigns whatever is returned to the return parameters. 

### Blank Returns - Never use these

```
func divAndRemainder(numerator, denominator int) (result int, remainder int,
                                                              err error) {
    if denominator == 0 {
        err = errors.New("cannot divide by zero")
        return
    }
    result, remainder = numerator/denominator, numerator%denominator
    return
}
```

If your function returns values, never use a blank return. It can make it very confusing to figure out what value is actually returned.




