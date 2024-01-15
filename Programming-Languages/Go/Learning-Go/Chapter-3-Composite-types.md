---
tags:
  - Go
  - Programming-Language
  - Golang
---
### Arrays - Too rigid to use directly

All of the elements in the array must be of the type that's specified. This does not mean they are always of the same type.
There are three declaration styles.

- In the first one, you specify the size and the type of the array
```
var x[3]int
```
In the aforementioned, the three elements of the array will be initialized to the default zero value for an int.
- If you have initial values for the array, you specify them with an array literal
```
var x = [3] int(10, 20, 30)
```
A **sparse array** is said to be **sparse** if most of its elements  are set to their zero value, therefore you can specify only the indices with values in the array literal
```
var x = [12]int(1, 5:4 ,6,10:100, 15)
```
which is create the following values
```
[1,0,0,0,4,6,0,0,0,100,15]
```
When using an array literal to initialize an array, you can leave off the number and use `...` instead
```
var x = [...]int(10,20,30)
```
which is equivalent to
```
var x = [3]int(10,20,30)
```

Go does not have support for matrix operations since it only has one-dimensional arrays. Still, you can simulate multidimensional arrays as follows:
```
var x [2][3]int
```
If you access an invalid array index there will be a compile-time error, if you use a variable index in out-of-bounds will fail in runtime with panic
- To get the length of the array use `len`
```
len(x)
```
**CAUTION**:
- Go arrays come with an "unusual limitation", go considers the size of the array to be part of the type of the array
- This means you cannot use a variable to specify the size of an array, because types must be resolved at compile time
- You can't use type conversion to convert arrays of different sizes to identical types.
### Slices

- If you use a data structure that holds a sequence of values a slice is what you should use
- The length is not part of the type for a slice 
- Working with slices is similar to working with arrays with a couple of differences, the first one we don't specify the size of the slice when is declared.
```
var x = []int(10,20,30)
```
Just like arrays we can define slice literal:
```
var x = {}int(1, 5:4, 6, 10:100, 15)
```
This will create a slice of 12 ints with the following values `[1,0,0,0,4,6,0,0,0,100,15]`
You can simulate multidimensional slices and make a slice of slices
```
var x [][]int
```

- One of the first differences with arrays can be observed when declaring slices without using a literal
```
var x []int
```
Since no value is assigned, x is assigned the zero value for a slice which is `nil`

- In Go, `nil` is an identifier that represents the lack of value for some types.
- Nil has no type
- Therefore, the only thing you can compare a slice with is nil:
```
fmt.Println(x == nil) // print true
```
Go provides seeveral built-in functions to work with its built-in types-

- **len**
- **append**
	- Used to grow slices
```
var x []int
x = append(x, 10)
```
The previous append 10 to a nil slice
```
var x = []int(1,2,3)
x = append(x,4)
```
The previous would append to a slice that has already elements

One slice is appended onto another by using the `...`operator to expand the source slice into individual values
```
y := []int(20,30,40)
x = append(x, y...)
```
### Capacity
Every slice has a  ***Capacity***, which is the number of consecutive memory locations reserved.
When the length reaches the capacity, and tries to add additional values, the **append** function uses the ***Go runtime*** to allocate a new slice with a larger capacity.

You can use it with the `cap`command

```
	var x []int
	fmt.Println(x, len(x), cap(x))
	x = append(x, 10)
	fmt.Println(x, len(x), cap(x))
	x = append(x, 20)
	fmt.Println(x, len(x), cap(x))
	x = append(x, 30)
	fmt.Println(x, len(x), cap(x))
	x = append(x, 40)
	fmt.Println(x, len(x), cap(x))
	x = append(x, 50)
	fmt.Println(x, len(x), cap(x))
```
Would output
```
[] 0 0
[10] 1 1
[10 20] 2 2
[10 20 30] 3 4
[10 20 30 40] 4 4
[10 20 30 40 50] 5 8
```
### make

If you want to specify the length or capacity you can use `make`
```
x := make([]int, 5)
```
This create an int slice with a length of 5 and a capacity of 5

To specify an initial capacity you here is an example
```
x := make([]int, 5, 10)
```
This has a length of 5 and capacity of 10

Also you can define a length of zero but still have capacity to not have nils

```
x := make([]int, 0, 10)
x = append(x, 5,6,7,8)
```
This would be a slice with `[5,6,7,8]`, a length of 4 and a capacity of 10

#### Declaring your slice

Declaring a slice that might stay nil

```
var data []int
```

Declare a non-nil zero-length slice 

```
var x = []int{}
```

Starting values of a slice that mgiht not change, slice literal

```
data := []int{2, 4, 6, 8}
```

### Slicing slices

A ***slice expression* creates a slice of a slice
```
	x := []int{1, 2, 3, 4}
	y := x[:2]
	z := x[1:]
	d := x[1:3]
	e := x[:]
	fmt.Println("x: ", x)
	fmt.Println("y: ", y)
	fmt.Println("z: ", z)
	fmt.Println("d: ", d)
	fmt.Println("e: ", e)
```
Would output
```
x:  [1 2 3 4]
y:  [1 2]
z:  [2 3 4]
d:  [2 3]
e:  [1 2 3 4]
```

When you take a slice of a slice, you are not making a copy of the data. Instead you now have two variables that are sharing memory.

```
	x := []int{1, 2, 3, 4}
	y := x[:2]
	z := x[1:]
	x[1] = 20
	y[0] = 10
	z[1] = 30
	fmt.Println("x: ", x)
	fmt.Println("y: ", y)
	fmt.Println("z: ", z)
	fmt.Println("x: ", x)
	fmt.Println("y: ", y)
	fmt.Println("z: ", z)
```
Will output
```
x:  [10 20 30 4]
y:  [10 20]
z:  [20 30 4]
x:  [10 20 30 4]
y:  [10 20]
z:  [20 30 4]
```
Changing x modified both y and z, while changes to y and z modified x

To void complicated slice situations, you should either never use append with a subslice.
### Converting Arrays to Slices

Taking a slice from an array has the same memory-sharing properties as taking a slice from a slice.

```
x := [4]int{1, 2, 3, 4}
y := x[:2]
z := x[2:]
```
### Copy

To create a slice independent of the original you can yous the built-in `copy` function.

```
x := []int{1, 2, 3, 4}
y := make([]int, 4)
num := copy(y, x)
fmt.Println(y, num) You get the output: [1 2 3 4] 4
```
Copy function takes two parameters the destination and the source slice, and return the number of elements copied

The copy function takes into account the length, the capacity not. So for example if we copy a 4 elements slice in a 2 we would get something as shown below.

```
x := []int{1, 2, 3, 4}
y := make([]int, 2)
num = copy(y, x)
```

y gets `[1 2]` and num is equal to 2

### String and Runes and Bytes

**NOTE**: A String in Go is **NOT** made of runes
Go Strings is composed of a sequence of UTF-8 encoded code points

```
var s string = "Hello there"
var b byte = s[6]
```

Go has some type conversion between runes, strings and bytes
A single rune or byte can be concerted to a string

```
var a rune    = 'x'
var s string  = string(a)
var b byte    = 'y'
var s2 string = string(b)

```

A string can be converted back and forth to a slice of bytes or runes:

```
var s string = "Hello, "
var bs []byte = []byte(s)
var rs []rune = []rune(s)
fmt.Println(bs)
fmt.Println(rs)

When you run this code, you see: 

[72 101 108 108 111 44 32 240 159 140 158]
[72 101 108 108 111 44 32 127774]

```
## Maps

The map type is written as \[ keyType \]valueType.

```
var nilMap map[string]int
```

The zero value for a map is nil

Attempting to write to a nil map variable causes panic

We can use a  `:=` declaration to create a map variable by assigning it a map literal

```
totalWins := map[string}int{}
```
this is what a nonempty map literal looks like

```
teams := map[string][]string {
    "Orcas": []string{"Fred", "Ralph", "Bijou"},
    "Lions": []string{"Sarah", "Peter", "Billie"},
    "Kittens": []string{"Waldo", "Raul", "Ze"},
}
```

Maps are like slices in several ways: 

- Maps automatically grow as you add key-value pairs to them. 
- If you know how many key-value pairs you plan to insert into a map, you can use make to create a map with a specific initial size. 
- Passing a map to the len function tells you the number of key-value pairs in a map. 
- The zero value for a map is nil. 
- Maps are not comparable. You can check if they are equal to nil, but you cannot check if two maps have identical keys and values using == or differ using !=.

The key for a map can be any comparable type. This means you cannot use a slice or a map as the key for a map.

Use a map when the order of elements doesn’t matter. Use a slice when the order of elements is important.

### Reading and Writing a Map

#### The comma ok Idiom

You can "unpack" (more returns two results the value of key if exists and true or false if key exists)

```
m := map[string]int{
    "hello": 5,
    "world": 0,
}
v, ok := m["hello"]
fmt.Println(v, ok)

v, ok = m["world"]
fmt.Println(v, ok)

v, ok = m["goodbye"]
fmt.Println(v, ok)

```

Will output

```
5 true 

0 true

0 false
```

To delete a key in a map you can use the `delete` in built method as shown below}

```
m := map[string]int{
    "hello": 5,
    "world": 10,
}
delete(m, "hello")
```

#### Using Maps as Sets

Go does not have set but you can simulate it using Map

```
intSet := map[int]bool{}
vals := []int{5, 10, 2, 5, 8, 7, 3, 9, 1, 2, 10}

for _, v := range vals {
    intSet[v] = true
}


fmt.Println(len(vals), len(intSet))
fmt.Println(intSet[5])
fmt.Println(intSet[500])
if intSet[100] {
    fmt.Println("100 is in the set")
}

```

Similarly we can use `struct ` 

```
intSet := map[int]struct{}{}
vals := []int{5, 10, 2, 5, 8, 7, 3, 9, 1, 2, 10}
for _, v := range vals {
    intSet[v] = struct{}{}
}

if _, ok := intSet[5]; ok {
    fmt.Println("5 is in the set")
}

```
## Structs

```

type person struct {
    name string
    age  int
    pet
```

A struct type is defined with the keyword type, the name of the struct type, the keyword struct, and a pair of braces ({}).

You can define a struct type inside or outside of a function. A struct type that’s defined within a function can only be used within that function.

Then we can use it as follow

```
julia := person{
    "Julia",
    40,
    "cat",
}
```

The second struct literal style looks like the map literal style:

```
beth := person{
    age:  30,
    name: "Beth",
}
```

### Anonymous Structs

You can also declare that a variable implements a struct type without first giving the struct type a name. This is called an anonymous struct:

```
var person struct {
    name string
    age  int
	pet  string
}

person.name = "bob"
person.age = 50
person.pet = "dog"

pet := struct {
    name string
    kind string
}{
    name: "Fido",
    kind: "dog",
}


```

### Comparing and converting structs

Whether or not a struct is comparable depends on the struct’s fields. Structs that are entirely composed of comparable types are comparable; those with slice or map fields are not

this: if two struct variables are being compared and at least one of them has a type that’s an anonymous struct, you can compare them without a type conversion if the fields of both structs have the same names, order, and types. You can also assign between named and anonymous struct types if the fields of both structs have the same names, order, and types:

```
type firstPerson struct {
    name string
    age  int
}
f := firstPerson{
    name: "Bob",
    age:  50,
}
var g struct {
    name string
    age  int
}

// compiles -- can use = and == between identical named and anonymous structs
g = f
fmt.Println(f == g)

```