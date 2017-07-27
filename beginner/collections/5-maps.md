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
- Navigable Map provides more features than Sorted Map
