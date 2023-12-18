---
tags:
  - Go
  - Programming-Language
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

