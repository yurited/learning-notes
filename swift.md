### Data structures

Four Essential Data structure-building concepts in Swift
- class
    reference type (classes are stored in the heap and are passed around via pointers)
    heap is automatically "kept clean" by swift (via reference counting, not garbage collection)
- struct
    value type (structs don't live in the heap and are passed aroucd by copying them)
    very efficient "copy on write" is automatic in Swift
    no in inheritance (of data)
    mutability controlled via let (e.g.you cannot add elements to an array assigned by let)
    supports functional programming design
    Examples: Array Dictionary, String, Character, Int, Double, UInt32
- enum

- protocol

### automatic reference counting
- reference types are stored in the heap
- the system counts references to each of them and when there are zero ref, they get tossed
- It is known as  "ARC" and it's not garbage collection

#### Influencing

##### strong
- strong is normal reference count
- as long as anyone, anywhere has a strong pointer to an instance, it will stay in the heap

##### Weak
- weak means if no one else is interested in this, then neither am I , set me to nil in that case
- because it has to be nil able weak only applies to Optional pointers to reference types
- A weak pointer will NEVER keep an object in the heap

- great example: outlets (strongly held by the view hierarchy, so outlets can be weak)

##### unowned
unowned means "don't reference count this; crash if i'm wrong"
this is very rarely used
usually only break memory cycles between objects (closures)


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


### Access Control

`internal` this is the default. useable by any object in my app or framework.

`private` - this means only callable from within this object

`private(set)` readonly outside

`fileprivate`

`public` (for frameworks readonly)

`open` (for frameworks readonly) public and objects outside my framework can subclass this


### Extensions

extending existing data structures
you can add methods/properties to a class/struct/enum (even if you don't have the source)

restrictions
- you can't re-implement methods or properties that are already there (only add new ones)
- the properties you add can have no storage associated with them

An extension from Int that returns a random number with in Range
example use: `5.arc4random`, `-4.arc4random`
```
extension Int {
    var arc4random: Int {
        if self > 0 {
            return Int(arc4random_uniform(UInt32(self)))
        } else if self < 0 {
            return -Int(arc4random_uniform(UInt32(abs(self))))
        } else {
            return 0
        }

    }
}
```

### enum

Another variety of data structure in addition to struct and class
Can only have discrete states
```
enum FastFoodMenuItem {
    case hamburger
    case fries
}
```
enum is a value type like struct, so it is copied as it is passed around

#### with associated data in swift

```
enum FastFoodMenuItem {
    case hamburger (numberOfPatties: Int)
    case fries(size: FryOrderSize)
    case drink(String, ounces: Int)
    case cookie

    func isIncludedInSpecialOrder(number: Int) -> Bool {
        switch self {
            case .hamburger(let pattyCount): return pattyCount == number
            case .fries, .cookie: return true
        }
    }

    var calories: Int {
        // calculate and return, no stored values
    }

    mutating func switchToBeingACookie() {
        // note that mutating is required because enum is a **value type**, copy on write
        self = .cookie
    }
}

enum FryOrderSize {
    case large
    case small
}
```

`let menuItem: FastFoodMenuItem = FastFoodMenuItem.hamburger(patties: 2)`

`var otherItem: FastFoodMenuItem = FastFoodMenuItem.cookie`

`var otherItem: FastFoodMenuItem = .cookie`

`var otherItem = FastFoodMenuItem.fries(size: .large) // swift knows .large is type FryOrderSize`

checking a enum:
```
switch menuItem { //must include every case
    case .hamburger: break
    case .fries: print("fries")
    case .drink(let brand, let ounces): print("a \(ounces) oz \(brand)") // getting associated data, name doesn't have to be same as they are declared
    default: print("other")
}
```


### Optional
```
var hello: String?              var hello: Optional<String> = .none
var hello: String? = "hello"    var hello: Optional<String> = .some("hello")
var hello: String? = nil        var hello: Optional<String> = .none
```

#### unwrapping:
```
print(hello!)
// equals to
switch hello:
    case .some(let data):
        print(data)
    case .none:
        //exception (crash)
```

`if let`

**nil-coalescing operator**

```
let y = x ?? "foo"
// equals to
switch x:
    case .none:
        y = "foo"
    case .some(let data):
        y = data
```


**optional chaining**

`let y = x?.foo()?.bar?.z`
