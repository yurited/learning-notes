
### Range

`0.5...15.25` is a Range but not a CountableRange

stride is a global function that will create a CountableRange from floating point values

```
for i in stride(from: 0.5, through: 15.25, by: 0.3) {

}
```
actually `ClosedCountableRange` in this case because it's `through:` instead of `to:`


### Tuples
```
let x: (String, Int, Double) = ("hello", 5, 0.85)
let (word, number, value) = x
print(word)
print(number)
print(value)

let x: (w: String, i: Int, v: Double) = ("hello", 5, 0.85)
print(x.w)
print(x.i)
print(x.v)
let (word, number, value) = x // also legal
```
good for returning multiple values

### Computed Properties
The value of a property can be computed rather than stored
```
var foo: Double
// A computed property

var foo: Double {
    get {
        // return calculated
    }
    set(newValue) {
    // or set { internal var will default to 'newValue'
        // do something
    }
}
```
don't have to implement the side side of it if you don't want to.
The property then becomes "read only"

> Lots of times a property is derived from other state
