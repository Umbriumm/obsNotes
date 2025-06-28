
- Initialization: 
``` java
Arraylist<Type> name = new ArrayList<>();
```
Where 'Type' is a Wrapper class (ex: Integer instead of int)

- Converts <mark style="background: #ADCCFFA6;">Primitive Types</mark> into <mark style="background: #ADCCFFA6;">Reference Types</mark> and stores them.
- the `.add` and `.get(index)` methods are used to add or get entries at indices.
- `array.length()` in arrays correspond to `list.size()` in lists.
- `.remove` removes, `.contains()` returns a boolean.
- **Strings:** `.split("")` takes a string around which the original string is going to be split and returns an array of the split parts.
----------------------------------------
#### Reading and Writing from a file

- `Scanner sc = new Scanner(Paths.get(filepath));` Scanner that reads files