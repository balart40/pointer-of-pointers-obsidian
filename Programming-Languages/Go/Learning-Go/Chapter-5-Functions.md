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

## Functions are values

The type of a function is built out of the keyword `func` and the types of the parameters and return values. This combination is called the signature of the function.

Using functions as values allows you to create function as shown below

```
func add(i int, j int) int { return i + j }
func sub(i int, j int) int { return i - j }
func mul(i int, j int) int { return i * j }
func div(i int, j int) int { return i / j }
```

And use it in maps as below

```
var opMap = map[string]func(int, int) int{
    "+": add,
    "-": sub,
    "*": mul,
    "/": div,
}
```

And finally you can use it as shown below

```
func main() {
    expressions := [][]string{
        []string{"2", "+", "3"},
        []string{"2", "-", "3"},
        []string{"2", "*", "3"},
		[]string{"2", "/", "3"},
        []string{"2", "%", "3"},
        []string{"two", "+", "three"},
        []string{"5"},
    }
    for _, expression := range expressions {
        if len(expression) != 3 {
            fmt.Println("invalid expression:", expression)
            continue
        }
        p1, err := strconv.Atoi(expression[0])
        if err != nil {
            fmt.Println(err)
            continue
        }
        op := expression[1]
        opFunc, ok := opMap[op]
        if !ok {
            fmt.Println("unsupported operator:", op)
            continue
        }
        p2, err := strconv.Atoi(expression[2])
        if err != nil {
            fmt.Println(err)
            continue
        }
        result := opFunc(p1, p2)
        fmt.Println(result)
    }
}
```

### Function type declarations

Just like you can use the type keyword to define a struct, you can use it to define a function type, too

```
type opFuncType func(int,int) int
```

then we can rewrite the opMap as below

```
var opMap = map[string]opFuncType {
    // same as before
}
```

### Anonymous Functions

Not only can you assign functions to variables, you can also define new functions within a function and assign them to variables.
Not only can you assign functions to variables, you can also define new functions within a function and assign them to variables.

```
func main() {
    for i := 0; i < 5; i++ {
        func(j int) {
            fmt.Println("printing", j, "from inside of an anonymous function")
        }(i)
    }
}
```

## Closures 

Functions declared inside of functions are special; they are `closures`. This is a computer science word that means that functions declared inside of functions are able to access and modify variables declared in the outer function.

### Passing functions as parameters

Since functions are values and you can specify the type of a function using its parameter and return types, you can pass functions as parameters into functions.

```
type Person struct {
    FirstName string
    LastName  string
    Age       int
}

people := []Person{
    {"Pat", "Patterson", 37},
    {"Tracy", "Bobbert", 23},
    {"Fred", "Fredson", 18},
}
fmt.Println(people)
```

Then we can sort by the attribute

```
// sort by last name
sort.Slice(people, func(i int, j int) bool {
    return people[i].LastName < people[j].LastName
})
fmt.Println(people)
```

Also we can do

```
// sort by age
sort.Slice(people, func(i int, j int) bool {
    return people[i].Age < people[j].Age
})
fmt.Println(people)
```

Which will print

```
[{Pat Patterson 37} {Tracy Bobbert 23} {Fred Fredson 18}]
[{Tracy Bobbert 23} {Fred Fredson 18} {Pat Patterson 37}]
[{Fred Fredson 18} {Tracy Bobbert 23} {Pat Patterson 37}]
```

### Returning functions from functions

Not only can you use a closure to pass some function state to another function, you can also return a closure from a function.

```
func makeMult(base int) func(int) int {
    return func(factor int) int {
        return base * factor
    }
}
```

We can use the aforementioned with

```
func main() {
    twoBase := makeMult(2)
    threeBase := makeMult(3)
    for i := 0; i < 3; i++ {
        fmt.Println(twoBase(i), threeBase(i))
    }
}
```

which will output

```
0 0
2 3
4 6
```

### Defer

There are a few more things that you should know about defer.

First, you can defer multiple closures in a Go function. 

They run in last-in-first-out order; the last defer registered runs first.

The code within defer closures runs after the return statement.


```

func main() {
    if len(os.Args) < 2 {
        log.Fatal("no file specified")
    }
    f, err := os.Open(os.Args[1])
    if err != nil {
        log.Fatal(err)
    }
    defer f.Close()
    data := make([]byte, 2048)
    for {
        count, err := f.Read(data)
        os.Stdout.Write(data[:count])
        if err != nil {
            if err != io.EOF {
                log.Fatal(err)
            }
            break
        }
    }
}

```

You can use the return named values as shown below

```
func DoSomeInserts(ctx context.Context, db *sql.DB, value1, value2 string)
                  (err error) {
    tx, err := db.BeginTx(ctx, nil)
    if err != nil {
        return err
    }
    defer func() {
        if err == nil {
            err = tx.Commit()
        }
        if err != nil {
            tx.Rollback()
        }
    }()
    _, err = tx.ExecContext(ctx, "INSERT INTO FOO (val) values $1", value1)
    if err != nil {
        return err
    }
    // use tx to do more database inserts here
    return
```

A common pattern in Go is for a function that allocates a resource to also return a closure that cleans up the resource.

```
func getFile(name string) (*os.File, func(), error) {
    file, err := os.Open(name)
    if err != nil {
        return nil, nil, err
    }
    return file, func() {
        file.Close()
    }, nil
}
```

Which we can use now

```
f, closer, err := getFile(os.Args[1])
if err != nil {
    log.Fatal(err)
}
defer closer()
```

## Go is call by value


```
type person struct {
    age  int
    name string
}
```

Then we use a function that modifies its vlues


```
func modifyFails(i int, s string, p person) {
    i = i * 2
    s = "Goodbye"
    p.name = "Bob"
}
```

when run 

```
func main() {
    p := person{}
    i := 2
    s := "Hello"
    modifyFails(i, s, p)
    fmt.Println(i, s, p)
}
```

which will output showing the modifications wont stick

```
2 Hello {0 }
```

for maps and slices this wont happen since they are  implemented with pointers

```
func modMap(m map[int]string) {
    m[2] = "hello"
    m[3] = "goodbye"
    delete(m, 1)
}

func modSlice(s []int) {
    for k, v := range s {
        s[k] = v * 2
    }
    s = append(s, 10)
} We then call these functions from main: func main() {
    m := map[int]string{
        1: "first",
        2: "second",
    }
	modMap(m)
    fmt.Println(m)

    s := []int{1, 2, 3}
    modSlice(s)
    fmt.Println(s)
}

```

which will output

```
map[2:hello 3:goodbye]
[2 4 6]

```