## Wildcards

- Used extensively
- (?)
- They can be bounded or unbounded
- Bounded:
  - Upper bounded: `List<? extends Cls>`
  - Lower bounded: `List<? super Cls>`
- Unbounded: `List<?>`
- get data with extends, put data with super
- use ? instead of ? extends Object
- get and put without wildcards

### Upper Bounded

- `? extends`
- Declares upper bound for the type parameter
- Usually to get data out of the parameter
- Parameter covariance
- Use instead of `<T extends Person>` when you will not use the type in the method's body
- If you need to use the type `T`, then you have to use `<T extends Person>`
- Like all other generic code, it saves you from copy/ paste code by reusing

```java
// You can pass any List as long as the type of the elements inherit (are subclass) the Person class OR are a Person
public void saveAll(final List<? extends Person> persons) throws IOException {
    // do something
}
```

### Lower Bounded

- `? super`
- Declare a lower bound for the type parameter
- used to put data into the parameter
- parameter contravariance

```java
// You can pass any List as long as the type of the elements are a parent of the Person class (Objects, etc)
public void loadAll(final List<? super Person> people) throws IOException {
    // save people from a Peson list into -> the passed peple list
}
```

### Unbounded

- `Class<?>` = `Class<? extends Object>`

```java

final String className = file.readUTF();
final String personName = file.readUTF();
final int age = file.readInt();

// personClass could be a class of any type
// Class<?> = class of any type
final Class<?> personClass = Class.forName(className);
```
