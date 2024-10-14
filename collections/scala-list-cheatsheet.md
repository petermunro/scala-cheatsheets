# Scala List Operations Cheatsheet

List in Scala is an immutable linked list. It's efficient for prepending elements and recursive algorithms. Here's a cheatsheet of common List operations with examples:

## Creating Lists

```scala
// Create a List with specified elements
val numbers = List(1, 2, 3, 4, 5)

// Create an empty List
val empty = List.empty[Int]

// Create a List with repeated elements
val repeatedFives = List.fill(5)(5) // List(5, 5, 5, 5, 5)

// Create a List from a range
val range = (1 to 5).toList // List(1, 2, 3, 4, 5)

// Create a List by tabulating a function
val squares = List.tabulate(5)(n => n * n) // List(0, 1, 4, 9, 16)

// Create a List using cons operator ::
val conslist = 1 :: 2 :: 3 :: Nil // List(1, 2, 3)
```

## Accessing Elements

```scala
val list = List(1, 2, 3, 4, 5)

// Access by index (0-based)
val third = list(2) // 3

// First and last elements
val first = list.head // 1
val last = list.last // 5

// Optional access
val maybeFirst = list.headOption // Some(1)
val maybeLast = list.lastOption // Some(5)

// Get List length
val length = list.length // 5

// Get all elements except the first
val tail = list.tail // List(2, 3, 4, 5)

// Get all elements except the last
val init = list.init // List(1, 2, 3, 4)
```

## Adding and Removing Elements

```scala
val list = List(1, 2, 3)

// Prepend element (efficient)
val prependedList = 0 :: list // List(0, 1, 2, 3)

// Append element (inefficient, creates a new list)
val appendedList = list :+ 4 // List(1, 2, 3, 4)

// Concatenate Lists
val combined = list ++ List(4, 5) // List(1, 2, 3, 4, 5)

// Remove first element
val tail = list.tail // List(2, 3)

// Remove last element
val init = list.init // List(1, 2)

// Update an element (returns a new List)
val updated = list.updated(1, 10) // List(1, 10, 3)
```

## Transforming Lists

```scala
val list = List(1, 2, 3, 4, 5)

// Map: apply a function to each element
val doubled = list.map(_ * 2) // List(2, 4, 6, 8, 10)

// FlatMap: map and flatten the result
val flatMapped = list.flatMap(x => List(x, x * 2)) // List(1, 2, 2, 4, 3, 6, 4, 8, 5, 10)

// Filter: keep elements that satisfy a predicate
val evens = list.filter(_ % 2 == 0) // List(2, 4)

// Collect: transform with partial function
val evenSquares = list.collect { case x if x % 2 == 0 => x * x } // List(4, 16)

// Zip: combine two lists
val zipped = list.zip(List("a", "b", "c", "d", "e")) // List((1,a), (2,b), (3,c), (4,d), (5,e))

// GroupBy: group elements by a function
val grouped = list.groupBy(_ % 2 == 0) // Map(false -> List(1, 3, 5), true -> List(2, 4))
```

## Aggregation and Folding

```scala
val list = List(1, 2, 3, 4, 5)

// Sum of all elements
val sum = list.sum // 15

// Product of all elements
val product = list.product // 120

// Fold (left to right)
val sumUsingFold = list.foldLeft(0)(_ + _) // 15

// Reduce (without initial value)
val sumUsingReduce = list.reduce(_ + _) // 15

// Scan: running totals
val runningSums = list.scan(0)(_ + _) // List(0, 1, 3, 6, 10, 15)
```

## Searching and Filtering

```scala
val list = List(1, 2, 3, 4, 5)

// Find the first element satisfying a predicate
val firstEven = list.find(_ % 2 == 0) // Some(2)

// Check if any element satisfies a predicate
val hasEven = list.exists(_ % 2 == 0) // true

// Check if all elements satisfy a predicate
val allPositive = list.forall(_ > 0) // true

// Count elements satisfying a predicate
val evenCount = list.count(_ % 2 == 0) // 2

// Get index of an element
val indexOfThree = list.indexOf(3) // 2

// Take first n elements
val firstThree = list.take(3) // List(1, 2, 3)

// Drop first n elements
val lastTwo = list.drop(3) // List(4, 5)
```

## Sorting and Ordering

```scala
val list = List(3, 1, 4, 1, 5, 9, 2, 6)

// Sort in ascending order
val sorted = list.sorted // List(1, 1, 2, 3, 4, 5, 6, 9)

// Sort in descending order
val descending = list.sortWith(_ > _) // List(9, 6, 5, 4, 3, 2, 1, 1)

// Sort by a key
case class Person(name: String, age: Int)
val people = List(Person("Alice", 30), Person("Bob", 25), Person("Charlie", 35))
val sortedByAge = people.sortBy(_.age) // List(Person("Bob", 25), Person("Alice", 30), Person("Charlie", 35))
```

## Conversion

```scala
val list = List(1, 2, 3, 4, 5)

// Convert to Vector
val vector = list.toVector // Vector(1, 2, 3, 4, 5)

// Convert to Array
val array = list.toArray // Array(1, 2, 3, 4, 5)

// Convert to Set
val set = list.toSet // Set(1, 2, 3, 4, 5)

// Convert to Map (with index as key)
val map = list.zipWithIndex.toMap // Map(1 -> 0, 2 -> 1, 3 -> 2, 4 -> 3, 5 -> 4)
```

Remember that List is immutable and has a linked structure. Prepending elements with `::` is efficient, but appending with `:+` or accessing by index are O(n) operations. For frequent random access or appends, consider using Vector instead.
