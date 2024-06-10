## Some Tips from Style principles
###  Simplicity
```go
// Good:
if err := doSomething(); err != nil {
    // ...
}

// Good:
if err := doSomething(); err == nil { // if NO error
    // ...
}
```

### Maintainability

```go
// Bad:
// The use of = instead of := can change this line completely.
if user, err = db.UserByID(userID); err != nil {
    // ...
}

// Good:
u, err := db.UserByID(userID)
if err != nil {
    return fmt.Errorf("invalid origin user: %s", err)
}
user = u

// Bad:
// The ! in the middle of this line is very easy to miss.
leap := (year%4 == 0) && (!(year%100 == 0) || (year%400 == 0))

// Good:
// Gregorian leap years aren't just year%4 == 0.
// See https://en.wikipedia.org/wiki/Leap_year#Algorithm.
var (
    leap4   = year%4 == 0
    leap100 = year%100 == 0
    leap400 = year%400 == 0
)
leap := leap4 && (!leap100 || leap400)
```

## Reference
https://google.github.io/styleguide/go/
https://google.github.io/styleguide/go/guide

