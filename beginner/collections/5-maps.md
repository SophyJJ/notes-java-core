## Maps

- Don't use the Dictionary class
- Only use the Map class
- YOu could use an ArrayList instead of a map, but performance would decrease by a lot
- Maps are very fast
- put will add or update value
- `Map` doesn't implement the `Collections` interface
- You can use views for Maps. `KeySet()`, `values()`, `entrySet()`. You can even modify the Map by removing elements from the views, but you cannot add elements to the Map

## Sorted Map and Navigable Map

- They are interfaces that extend the Map interface
- Sorted Map was added in Java 5 and Navigable Map was added to replace it with more features in Java 6
- They organize key=value pairs according to value of the key
- You have to provide a way to Compare the keys in order to sort the Map
- Navigable Map provides more features than Sorted Map. It replaces it.

## Java 8 Map Features

- Introduced in 2014

```java
// getOrDefault
// get value for key=10. If not in Map, return some default value
Product result = idToProduct.getOrDefault(10, defaultProduct);
// will not be null
System.out.println(result);

// replace
// replace the key-value pair where key=4 with a new value ONLY if that key exists
Product result = idToProduct.replace(4, new Product(1, "Something", 50));

// replaceAll
// replaces all the key=value pairs in the Map
// takes a lambda expression
// inputs are: vars for key and value
// output is: a new value to replace the older one
idToProduct.replaceAll((id, oldProduct) ->
    new Product(id, oldProduct.getName(), oldProduct.getWeight() + 10));

// computeIfAbsent
// get me the value where key=10. If absent, then add the key=10 with value=result of lambda
Product result = idToProduct.computeIfAbsent(10, (id) -> new Product(id, "Custom Product", 10));

// forEach
// in the past you had to use entrySet to get a view to loop over the Map's key=value pairs
// takes a callback (lambda expression) with key and value as inputs, so you can do whatever you want with them
// it will loop over all key=value pairs in the Map and call the labda expression
idToProduct.forEach((key, value) ->
{
    System.out.println(key + " -> " + value);
});
```

## Implementations (tradeoffs)

### HashMap

- General purpose Map implementation
- HashMap is array (buckets) of linked lists (changes to tree if number of collision is large)
- .hashcode() is obtained from the key and placed in some bucket (array entry) based on (hashcode_of_key % bucket_count)
- If # of collisions is small for a bucket, then elements are placed in linked list (where lookup = O(n))
- If # of collisions is large for a bucket, then linked list if converted to a tree (where lookup = O(logn))
- If the hashcodes change for keys in a HashMap, then the HashMap will never be able to find your elements. It will break
- Cannot use mutable keys in hashmaps. That's the contract for HashMap

### TreeMap

- Implements NavigableMap and SortedMap implementations (they are extensions of Map interface)
- Implemented with a red-black tree based on some order of the keys
- Keys need to be comparable (implement it if needed)
- A red-black tree is a kind of balanced binary tree. It will reorganize itself to always be balanced.
- red-black tree has a left and right subtrees (binary)

### LinkedHashMap

- Based on HashMap, but maintains an order
- Order can be based on insertion or access
- Very useful if you want to maintain the order of the elements you entered
- If you do it by access, you can override a method for it and remove the least recently used key=value pair
- You can use it to remove older entries on new insertions when you want to keep a fixed size
  - Gets called by put and putAll methods
  - Useful when implementing a cache

### WeakHashMap

- Weak references to its keys. It does not store the actual key objects, just references to those.
- If Java does garbage collection on that Key, then the key=value pair is removed from the WeakHashMap
- The key=values are removed when unreacheable
- Used maninly to implement a cache

### EnumMap

- Very special purpose
- Use ONLY if you have keys that are enums. Can't use it otherwise.
- Faster than other maps
- Implementation based upon bitsets
- Stores a single long for <= 64 elements


## Algorithmic Performance

- HashMap:
  - put: O(n), Omega(1)
  - get/conatinerKey: O(logn), Omega(1)
  - next: O(Capacity/n)

- LinkedHashMap:
  - put: O(n), Omega(1)
  - get/conatinerKey: O(logn), Omega(1)
  - next: O(Capacity/n)

- IdentityHashMap:
  - put: O(n), Omega(1)
  - get/conatinerKey: O(n), Omega(1)
  - next: O(Capacity/n)

- TreeMap:
  - put: O(logn)
  - get/conatinerKey: O(logn)
  - next: O(logn)

- EnumMap:
  - put: O(1)
  - get/conatinerKey: O(1)
  - next: O(1)
