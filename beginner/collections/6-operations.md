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

### Factories

- Static methods in the Collections calss to instantiate collections

```java
// singleton creates an immutable (cannot be modified at all) collections with 1 element
Set<Integer> set = Collections.singleton(1);
List<String> list = Collections.singletonList("one");
Map<Integer, String> map = Collections.singletonMap(1, "one");

// empty collections create immnutable empty collections
Set<Integer> set = Collection.emptySet();
List<String> list = Collection.emptyList();
Map<integer, String> map = Collections.emptyMap();

// unmodifiable => Creates a collection view that CANNOT be modified
private final List<Item> items = new ArrayList<Item>();
...
public List<Item> getItems() {
    // prevent from doing this and changing the original -> obj.getItems().add(new Item());
    // creates an unmodifiable view of items
    return Collections.unmodifiableList(items);
}
```

### Utilities

```java
// add elements item1, item2, and item3 into collection "items"
List<Item> items = new ArrayList<Item>();
Collections.addAll(items, item1, item2, item3);

// get minimum element in a collection
final Item minItem = Collections.min(items, Item.BY_PRICE);

// get maximum element in a collection
final Item maxItem = Collections.min(items, Item.BY_WEIGHT);
```
