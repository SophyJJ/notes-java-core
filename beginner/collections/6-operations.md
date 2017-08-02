## Collection Operations

- Opetarions available in `java.util.Collections`

### Algorithms


```java
// rotate = last element moves to first and pushes rest by one.
// repeat n times
Collections.rotate(yourCollection, n);

// radomly shuffle the collection.
// You can also pass a seed to get a deterministic results (for testing)
Collections.shuffle(yourCollection);

// sort based on your comparator
Collections.sort(yourCollection, yourComparator);

// on java 8, a sort method was added to the List interface. It might be faster.
yourCollection.sort(yourComparator);
```
