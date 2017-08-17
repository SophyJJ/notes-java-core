## Raw Types

- raw type => use of a generic type without using the generic parameter. ex "T"
- if you have raw types, then you have an unsafe scenario
- ex:

```java
// list using raw type (ie no generic type used)
List list = new ArrayList();
list.add("abc");
list.add(1);
list.add(new Object());

// This will blow up with ClassCastException
// this is the dangerous scenario
// now you have introduced a runtime error
List<String> strings = list;
for (String elem : strings) {
    System.out.println(elem);
}
```

### Erasure

- This is a process done by the compiler where it removed generics from source code and replaces them with raw types with casts in bytecode
- this is why you can't override method signatures that have List<> as params
- ex:
```java
// this will generate a compile time error
// error: Both errors have the same erasure3
// this is because the generics will be removed when compiled
public void print(List<String> param) {}
public void print(List<Integer> param) {}
```
- this means that generic types are all stripped at runtime, so you can't use them for anything dynamic
