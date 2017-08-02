# Lists

- collection with iteration order
- each element has an index based on position
- can hold duplicates
- to sort a List use a Comparator

```java

import java.util.Comparator;
import static java.util.Comparator.comparing;

// using Java 8
public class Product {
    // comparing and Product::getWeight are Java 8 features
    public static final Comparator<Product> BY_WEIGHT = comparing(Product::getWeight);
    private final String name;
    private final int weight;

    // getters and setters
}

// previous Java versions
public class Product {
    public static final Comparator<Product> BY_WEIGHT {
        public int compare(final Product p1, final Product p2) {
            return Integer.compare(p1.getWeight(), p2.getWeight());
        }
    };
    private final String name;
    private final int weight;

    // getters and setters
}
```

## List Implementations

### ArrayList

- backed by an array
- when you reach the end, the array doubles in size
- the array plays well with the CPU cache because pulled as contiguous memory
- good general purpose
- get: O(1) - good for getting an element. It jumps x memory locations (offset).
- add: O(N), omega(1) - when reaching List.size(), array has to copy all elements and double in size. But constant in average.
- contains: O(N) - has to go thorugh each element, but al least contiguous
- next: O(1) - just move to next memory location
- remove: O(N) - remove(O(1)) and then move all following elements' index (O(N))

### LinkedList

- backed by double linked list
- has pointers to tail and head
- each element points to prev and next
- not guaranteed to be contiguous
- get: O(N) - not as easy as jumping an offset. It has to go through all pointers.
- add: O(1) - when adding to end of list, then follow tail pointer, connect new item, and reassing tail pointer to new element
- contains: O(N) - has to jump through all pointers
- next: O(1) - follow pointer
- remove: O(1) - disconnect pointers (this does not count finding element)
