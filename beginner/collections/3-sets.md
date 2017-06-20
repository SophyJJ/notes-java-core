# Sets

- collections of distinct elements
- no duplicates

- they use the Equals/HashCode contract
  - if `object.equals(other)`, then `object.hashCode()` == `other.hashCode()`
  - when overriding `hashCode()`, you need to obtain the `hashCode` for all the instance vars
    - for objects, do: `result = 31 * result + obj.hashCode();`
    - for arrays, do: `Arrays.hashCode();`
    - for logs, do: `(int) (l ^ (l >>> 32));`
    - for floats, do: `Float.floatToIntBits(f);`
  - or... let your IDE do it for you
  - make sure you use the same instance vars in `equals` and `hashcode` to determine equality
  - since it's a math operation, it's possible that 2 different objects have the same `hashCode`
  - if using Java 7+, you can do:
  ```java

  public int equals(Object o) {
    // IDE generated code...

    // you can use equals from object class in the last step. It does null checking by default
    return Objects.equals(name, product.name);
  }
  public int hashCode() {
      // generate a hashcode based on fields that equals uses
      return Objects.hash(name, weight);
  }
  ```

## Implementations

### HashSet

- implement the `Set` interface
- built on top of a `HashMap` (key = hashcode, value = bucket)
- uses `hashCode()` of object being stored as key to store the value
- if multple objects have the same `hashCode` (ie collisions), then they will be placed in the same bucket
- uses `equals` to determine if object in the bucket
- you can override `hashCode()`
- good for general purpose
- override equals and hashcode to be value based
- add: O(N), omega(1) - worst case if all objects' hashcode have collisions. Very unlikely.
- contains: O(N), omega(1) - worst case if all objects' hashcode have collisions. Very unlikely.
- next: O(Capacity/N)

### TreeSet

- implement the `Set`, `SortedSet`, and `NavigableSet` interfaces
- built on top of a `TreeMap`
  - a `TreeMap` is a Binary tree that keeps left and right values (less than, greater than) and traverses according to order
  - a `TreeMap` requires that elements implement:
    - the `comparable` interface or
    - specify a `comparator` in the constructtor of the `TreeSet`
- add: O(log N) -> traverse from to top to bottom of tree
- contains: O(log N) -> traverse from to top to bottom of tree
- next: O(log N) -> traverse from to top to bottom of tree
- to use it, you need to implement `Comparator` for the object you are storing
- this is because the tree uses elements order
```java
import static java.util.Comparator.comparing;

public class Product {
    // using java 8 magic
    public static final Comparator<Product> BY_NAME = comparing(Product::getName);
}

// use it
private final Set<Product> products = new TreeSet<>(Product.BY_NAME);
```

### EnumsSet

- efficient with Enum types
- not general purpose
- used to store only enums
- built on top of a `BitSet`
- add: O(1) - bitwise operations with longs
- contains: O(1) - bitwise operations with longs
- next: O(1) - bitwise operations with longs

## SortedSet and NavigableSet

- collections with distinct elements that also have order
