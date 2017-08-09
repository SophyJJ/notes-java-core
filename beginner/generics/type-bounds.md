## Type Bounds

- Restrictions on the input type for the generic class
- You can specify that the type has to implement or extend some other type

```java
// generic class using type bounds
public class SortedPair<T extends Comparable<T>> {
    private final T first;
    private final T second;

    public SortedPair(T left, T right) {
        if (left.compareTo(right) < 0) {
            first = left;
            second = right;
        }
        else {
            first = right;
            second = left;
        }
    }
    public T getFirst() {
        return first;
    }
    public T getSecond() {
        return second;
    }
}

// tests
public class SortedPairTest {
    @Test
    public void shouldRetainOrderOfOrderedPair() {
        SortedPair<Integer> pair = new SortedPair<>(1, 2);
        assertEquals(1, pair.gerFirst().intValue());
        assertEquals(2, pair.getSecond().intValue());
    }

    @Test
    public void shouldFlipOrderOfMisorderedPair() {
        SortedPair<Integer> pair = new SortedPair<>(2, 1);
        assertEquals(1, pair.gerFirst().intValue());
        assertEquals(2, pair.getSecond().intValue());
    }
}
```
