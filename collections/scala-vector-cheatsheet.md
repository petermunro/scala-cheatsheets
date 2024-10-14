# Scala Vector Operations Cheatsheet

Vector in Scala is an immutable, indexed sequence with efficient append, prepend, and random access operations. Here's a cheatsheet of common Vector operations with examples:

## Creating Vectors

```scala
// Create a Vector with specified elements
val numbers = Vector(1, 2, 3, 4, 5)

// Create an empty Vector
val empty = Vector.empty[Int]

// Create a Vector with repeated elements
val repeatedFives = Vector.fill(5)(5) // Vector(5, 5, 5, 5, 5)

// Create a Vector from a range
val range = (1 to 5).toVector // Vector(1, 2, 3, 4, 5)

// Create a Vector by tabulating a function
val squares = Vector.tabulate(5)(n => n * n) // Vector(0, 1, 4, 9, 16)
```

## Accessing Elements

```scala
val vec = Vector(1, 2, 3, 4, 5)

// Access by index (0-based)
val third = vec(2) // 3

// First and last elements
val first = vec.head // 1
val last = vec.last // 5

// Optional access
val maybeFirst = vec.headOption // Some(1)
val maybeLast = vec.lastOption // Some(5)

// Slice
val slice = vec.slice(1, 4) // Vector(2, 3, 4)

// Get Vector length
val length = vec.length // 5
```

## Adding and Removing Elements

```scala
val vec = Vector(1, 2, 3)

// Add element at the end
val appendFour = vec :+ 4 // Vector(1, 2, 3, 4)

// Add element at the beginning
val prependZero = 0 +: vec // Vector(0, 1, 2, 3)

// Concatenate Vectors
val combined = vec ++ Vector(4, 5) // Vector(1, 2, 3, 4, 5)

// Remove first element
val tail = vec.tail // Vector(2, 3)

// Remove last element
val init = vec.init // Vector(1, 2)

// Update an element (returns a new Vector)
val updated = vec.updated(1, 10) // Vector(1, 10, 3)
```

## Transforming Vectors

```scala
val vec = Vector(1, 2, 3, 4, 5)

// Map: apply a function to each element
val doubled = vec.map(_ * 2) // Vector(2, 4, 6, 8, 10)

// FlatMap: map and flatten the result
val flatMapped = vec.flatMap(x => Vector(x, x * 2)) // Vector(1, 2, 2, 4, 3, 6, 4, 8, 5, 10)

// Filter: keep elements that satisfy a predicate
val evens = vec.filter(_ % 2 == 0) // Vector(2, 4)

// Collect: transform with partial function
val evenSquares = vec.collect { case x if x % 2 == 0 => x * x } // Vector(4, 16)

// Zip: combine two vectors
val zipped = vec.zip(Vector("a", "b", "c", "d", "e")) // Vector((1,a), (2,b), (3,c), (4,d), (5,e))
```

## Aggregation and Folding

```scala
val vec = Vector(1, 2, 3, 4, 5)

// Sum of all elements
val sum = vec.sum // 15

// Product of all elements
val product = vec.product // 120

// Fold (left to right)
val sumUsingFold = vec.foldLeft(0)(_ + _) // 15

// Reduce (without initial value)
val sumUsingReduce = vec.reduce(_ + _) // 15

// Aggregate: parallel reduction
val (count, sum) = vec.aggregate((0, 0))({ case ((c, s), x) => (c + 1, s + x) }, { case ((c1, s1), (c2, s2)) => (c1 + c2, s1 + s2) })
```

## Searching and Filtering

```scala
val vec = Vector(1, 2, 3, 4, 5)

// Find the first element satisfying a predicate
val firstEven = vec.find(_ % 2 == 0) // Some(2)

// Check if any element satisfies a predicate
val hasEven = vec.exists(_ % 2 == 0) // true

// Check if all elements satisfy a predicate
val allPositive = vec.forall(_ > 0) // true

// Count elements satisfying a predicate
val evenCount = vec.count(_ % 2 == 0) // 2

// Get index of an element
val indexOfThree = vec.indexOf(3) // 2
```

## Sorting and Ordering

```scala
val vec = Vector(3, 1, 4, 1, 5, 9, 2, 6)

// Sort in ascending order
val sorted = vec.sorted // Vector(1, 1, 2, 3, 4, 5, 6, 9)

// Sort in descending order
val descending = vec.sortWith(_ > _) // Vector(9, 6, 5, 4, 3, 2, 1, 1)

// Sort by a key
case class Person(name: String, age: Int)
val people = Vector(Person("Alice", 30), Person("Bob", 25), Person("Charlie", 35))
val sortedByAge = people.sortBy(_.age) // Vector(Person("Bob", 25), Person("Alice", 30), Person("Charlie", 35))
```

## Conversion

```scala
val vec = Vector(1, 2, 3, 4, 5)

// Convert to List
val list = vec.toList // List(1, 2, 3, 4, 5)

// Convert to Array
val array = vec.toArray // Array(1, 2, 3, 4, 5)

// Convert to Set
val set = vec.toSet // Set(1, 2, 3, 4, 5)

// Convert to Map (with index as key)
val map = vec.zipWithIndex.toMap // Map(1 -> 0, 2 -> 1, 3 -> 2, 4 -> 3, 5 -> 4)
```

Remember that Vector is immutable, so operations like `:+`, `+:`, and `updated` return new Vectors rather than modifying the original. This makes Vector an excellent choice for functional programming and when you need efficient random access and updates.
