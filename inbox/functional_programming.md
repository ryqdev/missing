
## Functional Programming

the principles of functional programming. Here's a brief overview:

- Immutable Data (No Mutable State): Functional programming emphasizes the use of immutable data. This means once a data structure is created, it cannot be changed. Any modifications result in new data structures being created. This approach avoids side effects and makes the behavior of programs more predictable and easier to understand.

- Explicit State (No Hidden State): In functional programming, the state is not hidden or implicit. Instead, functions operate on given inputs and produce outputs without relying on or altering hidden state. The lack of side effects and hidden state makes reasoning about code and debugging easier.

- Pure Functions: This is a key feature of functional programming. A function is considered pure if it always produces the same output for the same inputs and does not cause any side effects (like modifying global variables or outputting to a screen).

- First-Class and Higher-Order Functions: Functions are treated as first-class citizens, meaning they can be assigned to variables, passed as arguments, and returned from other functions. Higher-order functions, which take other functions as inputs or return them as outputs, are a common pattern in functional programming.

- Recursion Over Looping: Functional programming often favors recursion over traditional looping constructs, as looping inherently requires mutable state.

## FP examples

- Don’t Update, Create — String
```golang
//Wrong:
name := “Geison”
name := name + “ Flores”

//Right
const firstname = “Geison”
const lasname = “Flores”
const name = firstname + “ “ + lastname

```


- Don’t Update, Create — Arrays
```golang
// Wrong
years := [4]int{2001, 2002}
years[2] = 2003
years[3] = 2004
years // [2001, 2002, 2003, 2004]


// Right
years := [2]int{2001, 2002}
allYears := append(years, 2003, [2]int{2004, 2005})
```


- Don’t Update, Create — Maps
```golang
// Wrong
ages := map[string]int{“John”: 30}
ages[“Mary”] = 28
ages // {‘John’: 30, ‘Mary’: 28}


// Right

ages1 := map[string]int{“John”: 30}
ages2 := map[string]int{“Mary”: 28}
func mergeMaps(mapA, mapB map[string]int) map[string]int {
allAges := make(map[string]int, len(mapA) + len(mapB))
    for k, v := range mapA {
        allAges[k] = v
    }
    for k, v := range mapB {
        allAges[k] = v
    }
    return allAges
}
allAges := mergeMaps(ages1, ages2)

```

- Higher-Order Functions

Functions and methods are first-class objects in Golang, so if you want to pass a function to another function, you can just treat it like any other object.

```golang
func caller(f func(string) string) {
	result := f("David")
	fmt.Println(result)
}

func main() {
	f := func(name string) string {
		return "Hello " + name
	}
	caller(f)
}
```

## FP vs OOP

## Reference
https://medium.com/@geisonfgfg/functional-go-bc116f4c96a4



## FP in Golang
```golang
package main

import "log"

func checkAge(minAge int) func(age int) bool {
	return func(age int) bool {
		log.Println("age:", age)
		return age >= minAge
	}
}

func main() {
	checkAge18 := checkAge(18)
	log.Println(checkAge18(20))
}
```