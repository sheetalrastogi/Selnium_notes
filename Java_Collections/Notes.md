Count occurrences of a key in HashMap:
----------------------------------------

```java
import java.util.concurrent.ConcurrentHashMap;

public class RequestCounter {

	private static final ConcurrentHashMap<String, Integer> counterMap = new ConcurrentHashMap<>();

	public static void main(String[] args) {

		increment("PASS");
		increment("PASS");
		increment("FAIL");
		increment("PASS");

		System.out.println(counterMap);
	}

	public static void increment(String key) {

		counterMap.compute(key, (k, v) -> (v == null) ? 1 : v + 1);
	}
}
```


Output:
{PASS=3, FAIL=1}

## Useful ConcurrentHashMap Methods

- map.put(key, value);
- map.get(key);
- map.remove(key);

- map.putIfAbsent(key, value);

- map.compute(key, remappingFunction);

- map.computeIfAbsent(key, mappingFunction);   
Executes only if the key is missing.
```java
	map.computeIfAbsent("PASS",key -> 1);
	map.computeIfAbsent("PASS",key -> 100);
```  
Output:  {PASS=1}

- map.computeIfPresent(key, remappingFunction);
Executes only if the key already exists.

```java
map.put("PASS", 5);
map.computeIfPresent("PASS", (key, value) -> value + 1);
```

Output:  {PASS=6}

- map.merge(key, value, remappingFunction);
Inserts a value if the key does not exist.

If the key exists, combines old and new values using the provided function.

```java
 	map.merge("PASS", 1, Integer::sum);
	map.merge("PASS", 1, Integer::sum);
	map.merge("PASS", 1, Integer::sum);

	System.out.println(map);
```

Output:  {PASS=3}


- map.forEach((k, v) -> {});


## What is fail-fast behavior?

```java
Map<Integer,String> map = new HashMap<>();

Iterator<Integer> it = map.keySet().iterator();

map.put(1,"A");

it.next(); // Exception  ConcurrentModificationException
```


## Iterate Maps

```java
for (Map.Entry<String,Integer> e : map.entrySet()) {
    System.out.println(
        e.getKey() + " = " + e.getValue());
}
```


## Collections.synchronized(new HashMap....)

```java
import java.util.Collections;
import java.util.HashMap;
import java.util.Map;

public class SynchronizedMapExample {

    public static void main(String[] args) {

        Map<String, Integer> map = Collections.synchronizedMap(new HashMap<>());
        map.put("Apple", 10);
        map.put("Banana", 20);

        System.out.println(map.get("Apple"));
        System.out.println(map);
    }
}
```

## Shallow vs. Deep Copy

A HashMap shallow copy copies the map structure only, while the values (objects) are still shared between the original and copied map.

A deep copy creates new objects for both the map and its values, so changes in one map do not affect the other.

### Example Class

```java
class Employee {
	private int id;
	private String name;

	public Employee(int id, String name) {
		this.id = id;
		this.name = name;
	}

	public Employee(Employee e) { // Copy Constructor
		this.id = e.id;
		this.name = e.name;
	}

	public void setName(String name) {
		this.name = name;
	}

	@Override
	public String toString() {
		return id + " : " + name;
	}
}
```

### 1. Shallow Copy

Using:
- new HashMap<>(originalMap)
- putAll()
- clone()

```java
import java.util.HashMap;
import java.util.Map;

public class ShallowCopyExample {

	public static void main(String[] args) {

		Map<Integer, Employee> original = new HashMap<>();

		original.put(1, new Employee(101, "John"));

		// Shallow Copy
		Map<Integer, Employee> copied = new HashMap<>(original);

		System.out.println("Before Change:");
		System.out.println("Original = " + original);
		System.out.println("Copied   = " + copied);

		// Modify object through copied map
		copied.get(1).setName("Mike");

		System.out.println("\nAfter Change:");
		System.out.println("Original = " + original);
		System.out.println("Copied   = " + copied);
	}
}
```

Output

```text
Before Change:
Original = {1=101 : John}
Copied   = {1=101 : John}

After Change:
Original = {1=101 : Mike}
Copied   = {1=101 : Mike}
```

### 2. Deep Copy

Create new Employee objects while copying.

```java
import java.util.HashMap;
import java.util.Map;

public class DeepCopyExample {

	public static void main(String[] args) {

		Map<Integer, Employee> original = new HashMap<>();

		original.put(1, new Employee(101, "John"));

		// Deep Copy
		Map<Integer, Employee> copied = new HashMap<>();

		for (Map.Entry<Integer, Employee> entry : original.entrySet()) {
			copied.put(entry.getKey(), new Employee(entry.getValue()) // New Object
			);
		}

		System.out.println("Before Change:");
		System.out.println("Original = " + original);
		System.out.println("Copied   = " + copied);

		// Modify copied map object
		copied.get(1).setName("Mike");

		System.out.println("\nAfter Change:");
		System.out.println("Original = " + original);
		System.out.println("Copied   = " + copied);
	}
}
```
Output:

```text
Before Change:
Original = {1=101 : John}
Copied   = {1=101 : John}

After Change:
Original = {1=101 : John}
Copied   = {1=101 : Mike}
```



### Common Ways to Create a Shallow Copy

```java
	Map<Integer, Employee> copy1 = new HashMap<>(original);
	Map<Integer, Employee> copy2 = new HashMap<>();
	copy2.putAll(original);

	Map<Integer, Employee> copy3 = (HashMap<Integer, Employee>) ((HashMap<Integer, Employee>) original).clone();
```

