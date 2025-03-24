# Java Arrays and Collections

This comprehensive guide covers Java arrays and collections, explaining their syntax, usage patterns, and best practices.

## Table of Contents
- [Arrays](#arrays)
  - [Array Basics](#array-basics)
  - [Array Operations](#array-operations)
  - [Multidimensional Arrays](#multidimensional-arrays)
  - [Array Utility Methods](#array-utility-methods)
- [Collections Framework](#collections-framework)
  - [Collection Interfaces](#collection-interfaces)
  - [List Interface](#list-interface)
  - [Set Interface](#set-interface)
  - [Queue Interface](#queue-interface)
  - [Map Interface](#map-interface)
  - [Utility Classes](#utility-classes)
- [Arrays vs Collections](#arrays-vs-collections)
- [Common Algorithms](#common-algorithms)

## Arrays

### Array Basics

Arrays in Java are fixed-size, ordered collections of elements of the same data type. They store multiple values under a single variable name.

#### Declaration

```java
// Method 1 (preferred)
int[] numbers;

// Method 2 (alternative syntax)
int numbers[];
```

#### Initialization

```java
// 1. Declare and allocate memory
int[] numbers = new int[5];  // Creates array with 5 elements, initialized to 0

// 2. Declare, allocate memory, and initialize
int[] numbers = new int[] {10, 20, 30, 40, 50};

// 3. Shorthand initialization (only during declaration)
int[] numbers = {10, 20, 30, 40, 50};

// Arrays of other types
String[] names = {"Alice", "Bob", "Charlie"};
boolean[] flags = {true, false, true};
char[] letters = {'a', 'b', 'c'};
```

#### Accessing Elements

Java uses zero-based indexing for arrays:

```java
int[] numbers = {10, 20, 30, 40, 50};

// Read element
int first = numbers[0];     // Gets 10
int third = numbers[2];     // Gets 30

// Modify element
numbers[1] = 25;            // Changes 20 to 25

// Array length property
int length = numbers.length;  // Gets 5

// Last element
int last = numbers[numbers.length - 1];  // Gets 50
```

### Array Operations

#### Iterating Over Arrays

```java
int[] numbers = {10, 20, 30, 40, 50};

// Method 1: Standard for loop
for (int i = 0; i < numbers.length; i++) {
    System.out.println("Element at index " + i + ": " + numbers[i]);
}

// Method 2: Enhanced for loop (for-each)
for (int number : numbers) {
    System.out.println("Element: " + number);
}

// Method 3: Using Arrays.toString() to print entire array
System.out.println(Arrays.toString(numbers));  // Outputs: [10, 20, 30, 40, 50]
```

#### Copying Arrays

```java
int[] original = {1, 2, 3, 4, 5};

// Method 1: Using System.arraycopy()
int[] destination1 = new int[original.length];
System.arraycopy(original, 0, destination1, 0, original.length);

// Method 2: Using Arrays.copyOf()
int[] destination2 = Arrays.copyOf(original, original.length);

// Method 3: Using clone()
int[] destination3 = original.clone();

// Partial copy
int[] partialCopy = Arrays.copyOfRange(original, 1, 4);  // Creates [2, 3, 4]
```

### Multidimensional Arrays

Java implements multidimensional arrays as arrays of arrays.

#### Two-Dimensional Arrays

```java
// Declaration and memory allocation
int[][] matrix = new int[3][4];  // 3 rows, 4 columns

// Initialization with values
int[][] grid = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Accessing elements
int value = grid[1][2];  // Gets the value at row 1, column 2 (which is 6)

// Modifying elements
grid[0][0] = 10;  // Changes the value at row 0, column 0 to 10
```

#### Jagged Arrays (Irregular Arrays)

```java
// Declaration
int[][] jagged = new int[3][];

// Initialization of sub-arrays with different lengths
jagged[0] = new int[4];
jagged[1] = new int[2];
jagged[2] = new int[5];

// Or directly
int[][] jagged = {
    {1, 2, 3, 4},
    {5, 6},
    {7, 8, 9, 10, 11}
};
```

#### Iterating Over Multidimensional Arrays

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Using nested for loops
for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[i].length; j++) {
        System.out.print(matrix[i][j] + " ");
    }
    System.out.println();  // New line after each row
}

// Using enhanced for loops
for (int[] row : matrix) {
    for (int element : row) {
        System.out.print(element + " ");
    }
    System.out.println();
}

// Using Arrays.deepToString() for the entire matrix
System.out.println(Arrays.deepToString(matrix));
```

### Array Utility Methods

The `java.util.Arrays` class provides useful methods for array manipulation:

```java
int[] numbers = {5, 2, 9, 1, 7};

// Sorting an array
Arrays.sort(numbers);  // Modifies array to [1, 2, 5, 7, 9]

// Binary search (requires sorted array)
int index = Arrays.binarySearch(numbers, 5);  // Returns index of 5

// Filling an array
int[] zeros = new int[5];
Arrays.fill(zeros, 0);  // Sets all elements to 0

// Comparing arrays
int[] array1 = {1, 2, 3};
int[] array2 = {1, 2, 3};
boolean areEqual = Arrays.equals(array1, array2);  // Returns true

// Creating a fixed-size list from an array
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);
// Note: The resulting list is fixed-size and backed by the array

// Parallel operations (Java 8+)
Arrays.parallelSort(numbers);  // Parallel sorting
```

## Collections Framework

The Java Collections Framework provides a unified architecture for representing and manipulating collections of objects.

### Collection Interfaces

#### Core Interfaces Hierarchy

```
Collection
├── List
├── Set
│   └── SortedSet
│       └── NavigableSet
├── Queue
│   └── Deque
Map
├── SortedMap
│   └── NavigableMap
```

#### General Operations (Common to Most Collections)

```java
Collection<String> collection;  // Any collection implementation

// Basic operations
collection.add("Element");      // Add an element
collection.remove("Element");   // Remove an element
boolean contains = collection.contains("Element");  // Check if present
int size = collection.size();   // Get number of elements
boolean isEmpty = collection.isEmpty();  // Check if empty
collection.clear();             // Remove all elements

// Bulk operations
Collection<String> other = new ArrayList<>();
collection.addAll(other);       // Add all elements from other
collection.removeAll(other);    // Remove all elements found in other
collection.retainAll(other);    // Keep only elements found in other
boolean containsAll = collection.containsAll(other);  // Check if contains all

// Array operations
Object[] array = collection.toArray();  // Convert to Object array
String[] stringArray = collection.toArray(new String[0]);  // Convert to String array

// Iteration
for (String element : collection) {  // Using enhanced for loop
    System.out.println(element);
}

// Using iterator
Iterator<String> iterator = collection.iterator();
while (iterator.hasNext()) {
    String element = iterator.next();
    System.out.println(element);
    
    // Safe removal during iteration
    if (someCondition(element)) {
        iterator.remove();
    }
}
```

### List Interface

Lists are ordered collections that allow duplicate elements.

#### ArrayList

Resizable array implementation. Fast random access, slower modifications in the middle.

```java
// Creating ArrayList
List<String> names = new ArrayList<>();

// Adding elements
names.add("Alice");
names.add("Bob");
names.add("Charlie");
names.add(1, "David");  // Inserts at index 1

// Accessing elements
String first = names.get(0);  // Gets "Alice"
int index = names.indexOf("Bob");  // Gets index of "Bob"
int lastIndex = names.lastIndexOf("Alice");  // If duplicate elements exist

// Modifying elements
names.set(2, "Eve");  // Replaces element at index 2

// Removing elements
names.remove("Bob");       // Removes first occurrence
names.remove(0);           // Removes element at index 0

// Sublist (view of original list)
List<String> subList = names.subList(1, 3);  // Elements from index 1 (inclusive) to 3 (exclusive)

// Sorting
Collections.sort(names);  // Natural ordering
Collections.sort(names, Collections.reverseOrder());  // Reverse order
names.sort(Comparator.naturalOrder());  // Java 8+ method

// Converting to array
String[] array = names.toArray(new String[0]);
```

#### LinkedList

Doubly-linked list implementation. Fast insertions/deletions, slower random access.

```java
// Creating LinkedList
List<String> names = new LinkedList<>();

// Basic List operations are the same as ArrayList
names.add("Alice");
names.add("Bob");
names.add(1, "Charlie");

// LinkedList-specific operations (when using LinkedList reference)
LinkedList<String> linkedList = new LinkedList<>();
linkedList.addFirst("First");
linkedList.addLast("Last");
String first = linkedList.getFirst();
String last = linkedList.getLast();
linkedList.removeFirst();
linkedList.removeLast();
```

### Set Interface

Sets are collections that don't allow duplicate elements.

#### HashSet

Hash table implementation. Fast operations, no guaranteed order.

```java
// Creating HashSet
Set<String> uniqueNames = new HashSet<>();

// Adding elements (duplicates are ignored)
uniqueNames.add("Alice");
uniqueNames.add("Bob");
uniqueNames.add("Alice");  // Ignored, already exists
System.out.println(uniqueNames.size());  // Outputs 2

// Contains operation is very fast
boolean hasAlice = uniqueNames.contains("Alice");  // Returns true

// Iteration order is not guaranteed
for (String name : uniqueNames) {
    System.out.println(name);
}
```

#### LinkedHashSet

Hash table with linked list implementation. Maintains insertion order.

```java
// Creating LinkedHashSet
Set<String> orderedSet = new LinkedHashSet<>();

// Elements are stored in insertion order
orderedSet.add("Charlie");
orderedSet.add("Alice");
orderedSet.add("Bob");

// Iteration will follow insertion order: Charlie, Alice, Bob
for (String name : orderedSet) {
    System.out.println(name);
}
```

#### TreeSet

Red-black tree implementation. Elements are sorted (natural order or custom comparator).

```java
// Creating TreeSet (natural order)
Set<String> sortedNames = new TreeSet<>();
sortedNames.add("Charlie");
sortedNames.add("Alice");
sortedNames.add("Bob");

// Iteration will be in alphabetical order: Alice, Bob, Charlie
for (String name : sortedNames) {
    System.out.println(name);
}

// Creating TreeSet with custom comparator
Set<String> reverseSorted = new TreeSet<>(Collections.reverseOrder());

// For custom objects
Set<Person> sortedByAge = new TreeSet<>(Comparator.comparing(Person::getAge));

// TreeSet-specific operations (using TreeSet reference)
TreeSet<Integer> numbers = new TreeSet<>();
numbers.add(5);
numbers.add(1);
numbers.add(10);

Integer first = numbers.first();       // Gets smallest (1)
Integer last = numbers.last();         // Gets largest (10)
Integer ceiling = numbers.ceiling(6);  // Smallest element >= 6 (10)
Integer floor = numbers.floor(6);      // Largest element <= 6 (5)
```

### Queue Interface

Queues represent collections designed for holding elements prior to processing.

#### LinkedList (as Queue)

```java
// Creating Queue using LinkedList
Queue<String> queue = new LinkedList<>();

// Adding elements
queue.offer("First");   // Preferred method (returns false if queue full)
queue.add("Second");    // Throws exception if queue full

// Examining the head (without removing)
String peek = queue.peek();    // Returns null if empty
String element = queue.element();  // Throws exception if empty

// Removing and returning the head
String poll = queue.poll();    // Returns null if empty
String remove = queue.remove();  // Throws exception if empty
```

#### PriorityQueue

Heap-based implementation that orders elements by priority.

```java
// Creating PriorityQueue (natural order)
Queue<Integer> priorityQueue = new PriorityQueue<>();
priorityQueue.offer(5);
priorityQueue.offer(1);
priorityQueue.offer(10);

// Elements are dequeued in priority order
System.out.println(priorityQueue.poll());  // Outputs 1
System.out.println(priorityQueue.poll());  // Outputs 5
System.out.println(priorityQueue.poll());  // Outputs 10

// Custom priority ordering
Queue<Person> byAge = new PriorityQueue<>(Comparator.comparing(Person::getAge));
Queue<String> byLength = new PriorityQueue<>(Comparator.comparing(String::length)
                                            .thenComparing(Comparator.naturalOrder()));
```

#### Deque (Double-Ended Queue)

Interface for collections that support adding/removing from both ends.

```java
// Creating Deque using ArrayDeque
Deque<String> deque = new ArrayDeque<>();

// Adding elements
deque.addFirst("First");
deque.addLast("Last");
deque.offerFirst("New First");  // Similar but returns false instead of exception
deque.offerLast("New Last");    // when capacity restricted

// Examining elements (without removing)
String first = deque.getFirst();    // Throws exception if empty
String last = deque.getLast();      // Throws exception if empty
String peekFirst = deque.peekFirst();  // Returns null if empty
String peekLast = deque.peekLast();    // Returns null if empty

// Removing elements
deque.removeFirst();      // Throws exception if empty
deque.removeLast();       // Throws exception if empty
String pollFirst = deque.pollFirst();  // Returns null if empty
String pollLast = deque.pollLast();    // Returns null if empty

// Using as stack
deque.push("Top");        // Same as addFirst()
String top = deque.pop();  // Same as removeFirst()
```

### Map Interface

Maps associate keys with values. They don't implement Collection interface.

#### HashMap

Hash table implementation. Fast operations, no guaranteed order.

```java
// Creating HashMap
Map<String, Integer> scores = new HashMap<>();

// Adding key-value pairs
scores.put("Alice", 95);
scores.put("Bob", 85);
scores.put("Charlie", 90);

// Retrieving values
int bobScore = scores.get("Bob");  // Returns 85
Integer davidScore = scores.get("David");  // Returns null if key not found
int eveScore = scores.getOrDefault("Eve", 0);  // Returns 0 if key not found

// Checking for keys and values
boolean hasAlice = scores.containsKey("Alice");  // Returns true
boolean has90 = scores.containsValue(90);        // Returns true

// Updating values
scores.put("Bob", 88);  // Replaces old value
scores.putIfAbsent("David", 75);  // Adds only if key doesn't exist

// Removing entries
scores.remove("Charlie");            // Removes entry for key
scores.remove("Bob", 85);            // Removes only if key maps to specified value

// Size operations
int size = scores.size();
boolean isEmpty = scores.isEmpty();
scores.clear();

// Iteration
for (String name : scores.keySet()) {
    System.out.println("Key: " + name);
}

for (Integer score : scores.values()) {
    System.out.println("Value: " + score);
}

for (Map.Entry<String, Integer> entry : scores.entrySet()) {
    System.out.println(entry.getKey() + " scored " + entry.getValue());
}

// Java 8+ forEach
scores.forEach((name, score) -> {
    System.out.println(name + " scored " + score);
});
```

#### LinkedHashMap

Hash table and linked list implementation. Maintains insertion order.

```java
// Creating LinkedHashMap
Map<String, Integer> orderedScores = new LinkedHashMap<>();
orderedScores.put("Charlie", 90);
orderedScores.put("Alice", 95);
orderedScores.put("Bob", 85);

// Iteration will follow insertion order: Charlie, Alice, Bob
for (Map.Entry<String, Integer> entry : orderedScores.entrySet()) {
    System.out.println(entry.getKey());
}

// Access-order LinkedHashMap (maintains order of access, most recently accessed last)
Map<String, Integer> accessOrderMap = new LinkedHashMap<>(16, 0.75f, true);
```

#### TreeMap

Red-black tree implementation. Keeps keys sorted.

```java
// Creating TreeMap (natural order of keys)
Map<String, Integer> sortedScores = new TreeMap<>();
sortedScores.put("Charlie", 90);
sortedScores.put("Alice", 95);
sortedScores.put("Bob", 85);

// Iteration will follow the natural order of keys: Alice, Bob, Charlie
for (String name : sortedScores.keySet()) {
    System.out.println(name);
}

// TreeMap with custom comparator
Map<Person, String> personMap = new TreeMap<>(Comparator.comparing(Person::getAge));

// TreeMap-specific operations
TreeMap<String, Integer> treeMap = new TreeMap<>();
treeMap.put("Apple", 1);
treeMap.put("Banana", 2);
treeMap.put("Orange", 3);
treeMap.put("Pear", 4);

Map.Entry<String, Integer> firstEntry = treeMap.firstEntry();  // Smallest key
Map.Entry<String, Integer> lastEntry = treeMap.lastEntry();    // Largest key
Map.Entry<String, Integer> ceiling = treeMap.ceilingEntry("Grape");  // Smallest key >= "Grape"
Map.Entry<String, Integer> floor = treeMap.floorEntry("Grape");      // Largest key <= "Grape"
```

### Utility Classes

#### Collections Class

Provides static methods for collection operations:

```java
List<String> names = new ArrayList<>(Arrays.asList("Charlie", "Alice", "Bob"));

// Sorting
Collections.sort(names);  // Natural order
Collections.sort(names, Collections.reverseOrder());  // Reverse order

// Searching (requires sorted list for binary search)
int index = Collections.binarySearch(names, "Bob");

// Minimum and maximum
String min = Collections.min(names);
String max = Collections.max(names);

// Shuffling
Collections.shuffle(names);

// Frequency and disjoint
int frequency = Collections.frequency(names, "Alice");
boolean disjoint = Collections.disjoint(names, anotherCollection);  // True if no common elements

// Immutable views
List<String> unmodifiableList = Collections.unmodifiableList(names);
Set<String> singleton = Collections.singleton("Only Element");

// Thread-safe views
List<String> synchronizedList = Collections.synchronizedList(new ArrayList<>());
Map<String, Integer> synchronizedMap = Collections.synchronizedMap(new HashMap<>());
```

#### Immutable Collections (Java 9+)

```java
// Creating immutable collections
List<String> list = List.of("one", "two", "three");
Set<String> set = Set.of("one", "two", "three");
Map<String, Integer> map = Map.of(
    "one", 1,
    "two", 2,
    "three", 3
);

// For larger maps
Map<String, Integer> largeMap = Map.ofEntries(
    Map.entry("one", 1),
    Map.entry("two", 2),
    Map.entry("three", 3),
    // ... more entries
);
```

#### Stream API (Java 8+)

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");

// Filtering
List<String> filteredNames = names.stream()
    .filter(name -> name.length() > 3)
    .collect(Collectors.toList());

// Mapping
List<Integer> nameLengths = names.stream()
    .map(String::length)
    .collect(Collectors.toList());

// Sorting
List<String> sortedNames = names.stream()
    .sorted()
    .collect(Collectors.toList());

// Reducing
int totalLength = names.stream()
    .mapToInt(String::length)
    .sum();

// Grouping
Map<Integer, List<String>> byLength = names.stream()
    .collect(Collectors.groupingBy(String::length));

// Joining
String joined = names.stream()
    .collect(Collectors.joining(", "));
```

## Arrays vs Collections

### When to Use Arrays

- When size is fixed and known in advance
- For primitive types (to avoid boxing/unboxing overhead)
- When performance is critical (arrays have less overhead)
- When multidimensional structure is needed
- When working with low-level APIs that require arrays

### When to Use Collections

- When size needs to change dynamically
- When you need rich operations (sorting, searching, filtering)
- When you need specialized collection behaviors (uniqueness, ordering, etc.)
- When you need to store objects only (not primitives directly)
- When you need key-value associations (Maps)
- When you need thread-safe collections

## Common Algorithms

### Sorting

```java
// Array sorting
int[] numbers = {5, 2, 9, 1, 3};
Arrays.sort(numbers);  // In-place sort

// Partial array sorting
Arrays.sort(numbers, 1, 4);  // Sort from index 1 (inclusive) to 4 (exclusive)

// Collection sorting
List<String> names = new ArrayList<>(List.of("Charlie", "Alice", "Bob"));
Collections.sort(names);  // Natural order

// Custom sorting with Comparator
Collections.sort(names, (a, b) -> b.length() - a.length());  // By length descending

// Using Java 8+ methods
names.sort(Comparator.naturalOrder());
names.sort(Comparator.reverseOrder());
names.sort(Comparator.comparing(String::length));
```

### Searching

```java
// Linear search in array
int[] numbers = {5, 2, 9, 1, 3};
int index = -1;
for (int i = 0; i < numbers.length; i++) {
    if (numbers[i] == 9) {
        index = i;
        break;
    }
}

// Binary search in sorted array
Arrays.sort(numbers);
int binaryIndex = Arrays.binarySearch(numbers, 9);

// Collection searching
List<String> names = List.of("Alice", "Bob", "Charlie");
boolean containsBob = names.contains("Bob");
int bobIndex = names.indexOf("Bob");
```

### Filtering

```java
// Traditional filtering
List<String> names = new ArrayList<>(List.of("Alice", "Bob", "Charlie"));
List<String> longNames = new ArrayList<>();
for (String name : names) {
    if (name.length() > 3) {
        longNames.add(name);
    }
}

// Java 8+ Stream filtering
List<String> streamFiltered = names.stream()
    .filter(name -> name.length() > 3)
    .collect(Collectors.toList());
```

### Transforming

```java
// Traditional transformation
List<String> names = List.of("Alice", "Bob", "Charlie");
List<Integer> lengths = new ArrayList<>();
for (String name : names) {
    lengths.add(name.length());
}

// Java 8+ Stream mapping
List<Integer> streamMapped = names.stream()
    .map(String::length)
    .collect(Collectors.toList());
```

### Aggregating

```java
// Traditional sum calculation
List<Integer> numbers = List.of(1, 2, 3, 4, 5);
int sum = 0;
for (int number : numbers) {
    sum += number;
}

// Java 8+ Stream reduction
int streamSum = numbers.stream().mapToInt(Integer::intValue).sum();
double average = numbers.stream().mapToInt(Integer::intValue).average().orElse(0);
int max = numbers.stream().mapToInt(Integer::intValue).max().orElse(0);
```
