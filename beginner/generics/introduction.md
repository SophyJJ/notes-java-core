## Generics

- Generics stop runtime errors at compile time
- Generics provide type safety
- Ex: Collections are heterogeneous:
```java

// without using Generics
List list = new ArrayList();
list.add("1");
list.add("2");
list.add(3);
// if you were expecting all to be Strings, then your code will fail at runtime

// using generics to enforce type safety
List <String> list = new ArrayList<String>();
```

-
