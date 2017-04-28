# Data Types


## Strings
- Strings use UTF-16 encoding. They can represent everything.
- they are immutable
- everyime you change a string, a new one is created in the background
- use String.intern() instead of String.equals() when doing lots of comparisons
  - inter() will search for the string in a pool and return a reference to it
  - if none is found, then it will add the string to a pool and return a reference
  - you can use "==" to do reference comparison instead of .equals(), which is expensive
- string builder provides a mutable string buffer -> better performance than concatenation
  - even better is to give it a static size. It will grow after that (no overhead)
  - append and insert (at specifgic location) are most commonly used

## Primitive Wrapper classes

- all immutable
- there are clases representations for ALL primitive types
- They are lightweight (little overhead)
- you have access to their public instance vars and methods
- you can now use polymorphism on them (`Object obj = 100;`)
- conversions between primitive <-> wrapper class are done implicitely by Java
- you can convert expliticely as well:
  - primitive -> wrapper: boxing (using valueOf())
  - wrapper -> primitive: unboxing (xxxValue())
- Now you can use null for them. Much better when checking if a value has been set
- need to use .`equals()` when outside of some range (+/-127 for ints). Otherwise `==` is ok

## final and static final

- 2 types of final fields:
  - final fields that can only be set in constructor, field initializer, or init block and nowhere else
    - ex: `private final varTobeSetAtConstructor;`
  - static final fields -> these are constants. Cannot be changed and tied to class.
    - `static final CONSTANT = 100;`

- you can use enum types in a switch by only using thier names without enum type
