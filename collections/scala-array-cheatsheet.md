# Scala Array Operations Cheatsheet

Arrays in Scala are mutable, fixed-size data structures. Here's a cheatsheet of common Array operations with examples:

## Creating Arrays

```scala
// Create an array with specified elements
val numbers = Array(1, 2, 3, 4, 5)

// Create an array of a specific size, initialized with default values
val zeros = new Array[Int](5) // Array(0, 0, 0, 0, 0)

// Create an array and initialize with a value
val fives = Array.fill(5)(5) // Array(5, 5, 5, 5, 5)

// Create an array from a range
val range = Array.range(1, 6) // Array(1, 2, 3, 4, 5)

// Create a 2D array
val matrix = Array.ofDim[Int](3, 3)
```

## Accessing and Modifying Elements

```scala
val arr = Array(1, 2, 3, 4, 5)

// Access an element (0-based index)
val third = arr(2) // 3

// Modify an element
arr(1) = 10 // arr is now Array(1, 10, 3, 4, 5)

// Get first and last elements
val first = arr.head // 1
val last = arr.last // 5

// Get array length
val length = arr.length // 5
```

## Array Operations

### Transforming Arrays

```scala
val arr = Array(1, 2, 3, 4, 5)

// Map: apply a function to each element
val doubled = arr.map(_ * 2) // Array(2, 4, 6, 8, 10)

// Filter: keep elements that satisfy a predicate
val evens = arr.filter(_ % 2 == 0) // Array(2, 4)

// FlatMap: map and flatten the result
val flatMapped = arr.flatMap(x => Array(x, x * 2)) // Array(1, 2, 2, 4, 3, 6, 4, 8, 5, 10)
```

### Aggregation and Folding

```scala
val arr = Array(1, 2, 3, 4, 5)

// Sum of all elements
val sum = arr.sum // 15

// Product of all elements
val product = arr.product // 120

// Fold (left to right)
val sumUsingFold = arr.foldLeft(0)(_ + _) // 15

// Reduce (without initial value)
val sumUsingReduce = arr.reduce(_ + _) // 15
```

### Searching and Filtering

```scala
val arr = Array(1, 2, 3, 4, 5)

// Find the first element satisfying a predicate
val firstEven = arr.find(_ % 2 == 0) // Some(2)

// Check if any element satisfies a predicate
val hasEven = arr.exists(_ % 2 == 0) // true

// Count elements satisfying a predicate
val evenCount = arr.count(_ % 2 == 0) // 2

// Get index of an element
val indexOfThree = arr.indexOf(3) // 2
```

### Sorting and Ordering

```scala
val arr = Array(3, 1, 4, 1, 5, 9, 2, 6)

// Sort in place
scala.util.Sorting.quickSort(arr) // arr is now Array(1, 1, 2, 3, 4, 5, 6, 9)

// Create a sorted copy
val sortedCopy = arr.sorted // Array(1, 1, 2, 3, 4, 5, 6, 9)

// Sort in descending order
val descending = arr.sortWith(_ > _) // Array(9, 6, 5, 4, 3, 2, 1, 1)
```

### Conversion and Copying

```scala
val arr = Array(1, 2, 3, 4, 5)

// Convert to List
val list = arr.toList // List(1, 2, 3, 4, 5)

// Convert to Vector
val vector = arr.toVector // Vector(1, 2, 3, 4, 5)

// Create a copy
val copy = arr.clone()

// Create a slice
val slice = arr.slice(1, 4) // Array(2, 3, 4)
```

### Multi-dimensional Array Operations

```scala
val matrix = Array.ofDim[Int](3, 3)

// Set value in 2D array
matrix(0)(0) = 1

// Access value in 2D array
val value = matrix(0)(0) // 1

// Flatten a 2D array
val flattened = matrix.flatten
```

Remember that Arrays in Scala are mutable, so many operations modify the original array. When you need an immutable indexed sequence, consider using Vector instead.
