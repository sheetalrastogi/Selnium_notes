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






