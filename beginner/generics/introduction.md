## Generics

- Generics allow you to write generic code that can handle multiple types by receiving the type as input in <>
- Diamond operator <> was added in Java 7
- You can have as many generics as you want (but usualy try to keep it under 3)
- Generics provide type safety by producing compile time errors instead of run time errors when there is type issues
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

- Writing a generic class using Generics

```java
public class CircularBuffer<T> {
    private T[] buffer;
    private int readCursor = 0;
    private int writeCursor = 0;

    public CircularBuffer(T value) {
        buffer = (T[]) new Object[size];
    }
}
```
