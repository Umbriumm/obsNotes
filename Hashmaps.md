
- A way to structure data by mapping keys to values
- When a HashMap is initiated, JVM creates 16 **Buckets** (A LinkedList, in which a data element points to the next one) 
- The `hashcode()` operation determines which **Bucket** the object goes into (bucket index), via this expression:
``` java
object.hashcode() % n     /// Where n = total number of buckets (size)
```

- **Hash Collision:** When 2 distinct objects have the same <span style="color:rgb(192, 0, 0)">Hash Value</span>, the object gets added to the same **Bucket** as the first object, but the first object (node in the linked list) points the second object that just got added.
  When searching for the second object, the keys are compared to determine whether it's the one requested or not.
- **Load Factor:** When a HashMap exceeds 75% of it's capacity, it doubles.


![[Pasted image 20250207223414.png]]

- The default `hashcode()` function relies on an object's <span style="color:rgb(192, 0, 0)">reference</span> to give it a bucket's index.
```java
HashMap<Book, String> borrowers = new HashMap<>();

Book bookObject = new Book("Book Object", 2000, "...");
borrowers.put(bookObject, "Pekka");
borrowers.put(new Book("Test Driven Development", 1999, "..."), "Arto");

System.out.println(borrowers.get(bookObject));
System.out.println(borrowers.get(new Book("Book Object", 2000, "...")));
System.out.println(borrowers.get(new Book("Test Driven Development", 1999, "...")));

//// Output ////
pekka
null
null
```

The `hashcode()` and `equals()` methods can be modified to alter this behavior.
- The `hashcode()` method can be overridden to generate a hash from an object's fields
```java
public int hashCode() {
        return Objects.hash(day, month, year);    /// day, month, year are fields
    }
```
Or manually implement the hashing function.
>We must override `hashCode()` in every class that overrides `equals()` so that equal objects always hash to the same bucket in hash-based collections

-------------------------------------------------------------------

```java
HashMap<keyType, valueType> mapName = new HashMap<>();
mapName.put(key, value); // adds a value to a map
mapName.get(key); // returns the value at the key
```

- `mapName.get(key);` returns the value at that key (pay attention to the type of the key, if for example, the key is a string, then they key must be between quotes)
- If the hash map does not contained the key used for the search, its `get` method returns a `null` reference.
- A key corresponds to one value, if a new value is entered with an already-existing key, the new value <mark style="background: #FF5582A6;">overwrites the old one</mark>.
- **HashMaps** applies a hashing function to convert a key down to an index where the corresponding value is stored.
- `map.containskey(key)` >>> boolean
- `Set<String> keys = map.keySet();`  >>> returns a subset of the hashmap
	 Can be used to iterate over to search for a part of the string in the map	 ````
```java
ArrayList<Book> books = new ArrayList<>();

    for(String bookTitle : this.directory.keySet()) {
        if(!bookTitle.contains(titlePart)) {
            continue;
        }

        // if the key contains the given string
        // we retrieve the value related to it
        // and add it tot the set of books to be returned

        books.add(this.directory.get(bookTitle));
    }

    return books;
```

<mark style="background: #FF5582A6;">This way, however, we lose the speed advantage of the hashmap. As this method goes over all the entries in search of one. </mark>

- Similarly, `Collection<type> values = map.values();` returns a `Collection` of values of a HashMap that can be iterated through using a <mark style="background: #FFB86CA6;">for each loop</mark>
<mark style="background: #ABF7F7A6;">ex:</mark>
```java
for(String s : map.values()){}
```

| Feature        | `Collection`                                   | `Set`                                                                 |
| -------------- | ---------------------------------------------- | --------------------------------------------------------------------- |
| **Definition** | Root interface for all collections             | A special type of `Collection` that stores **unique elements / keys** |
| **Duplicates** | ✅                                              | ❌                                                                     |
| **Methods**    | `add()`, `remove()`, `size(), clear(), etc...` | Same as `Collection` but ensures uniqeness                            |

> **HashMaps** are most effective when searching by a certain key, but when searching for an entry that, for example, contains a String, we must search and iterate *through the whole HashMap* (eg, using a for:each loop), and that results in <mark style="background: #FF5582A6;">not taking advantage of the</mark> **HashMap's** <mark style="background: #FF5582A6;"> fast lookups.</mark>


- A **HashMap** expects only Reference type variables

- Java automatically converts primitives to references as they are added to either a **HashMap** or an **ArrayList** via **Wrapper Classes** (Autoboxing: works in both ways) 
```java
int key = 2;
HashMap<Integer, Integer> hashmap = new HashMap<>();
hashmap.put(key, 10);
int value = hashmap.get(key);
System.out.println(value);
```

- The `getOrDefault` method allows you to safely retrieve a value from a `HashMap` with a default value if the key doesn't exist, preventing `NullPointerException` issues and simplifying your code.
```java
getOrDefault(key, default);
```

---
