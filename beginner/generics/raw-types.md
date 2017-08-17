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
