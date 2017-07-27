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
