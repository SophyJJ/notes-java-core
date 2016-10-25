 ## Inner Classes
- Inner class = nested class
- Three main cases

### 1. Member Inner Class
- Used to logically separate code in a class. Each group = 1 inner class.
- Ex: Robot class may contain inner classes: brain, arms, legs, power
- Can access all instance variables (even private ones)
- Usually accessed only by outer class, but can be accessed outside.
``` java
// inside outer class
Inner inside = new Inner();

// outside outer class (if inner class is public of course)
// Not very common
Outer outerInst = new Outer();
Outer.Inner outside = outerInst.new Inner();
```
- If needed by external class, usually the outer class will create the inner class instance and return it to the external class.

### 2. Static Inner Class
- Cannot access non-static instance variables
- It's an inner class that is not associated to instances of outer class
- Common to be accessed by external classes
``` java
// assumes public
Outer.Inner staticInst = new Outer.Inner(); 
```

### 3. Anonymous Inner Class
