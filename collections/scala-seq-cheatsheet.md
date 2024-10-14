# Scala Seq Operations Cheatsheet

Scala's `Seq` is a trait for indexed sequences. Here are some common operations with examples:

## Creating Sequences

```scala
// Create an immutable sequence
val immutableSeq: Seq[Int] = Seq(1, 2, 3, 4, 5)

// Create a mutable sequence
import scala.collection.mutable.Seq
val mutableSeq: Seq[Int] = Seq(1, 2, 3, 4, 5)
```

## Basic Operations

### Accessing Elements

```scala
val seq = Seq(1, 2, 3, 4, 5)

// Access by index
val thirdElement = seq(2) // 3

// First and last elements
val first = seq.head // 1
val last = seq.last // 5

// Optional access
val maybeFirst = seq.headOption // Some(1)
val maybeLast = seq.lastOption // Some(5)
```

### Adding and Removing Elements

```scala
val seq = Seq(1, 2, 3)

// Add element at the end
val seqWithFour = seq :+ 4 // Seq(1, 2, 3, 4)

// Add element at the beginning
val seqWithZero = 0 +: seq // Seq(0, 1, 2, 3)

// Concatenate sequences
val combinedSeq = seq ++ Seq(4, 5) // Seq(1, 2, 3, 4, 5)

// Remove first element
val tail = seq.tail // Seq(2, 3)

// Remove last element
val init = seq.init // Seq(1, 2)
```

## Transforming Sequences

### Map

```scala
val seq = Seq(1, 2, 3, 4, 5)
val doubled = seq.map(_ * 2) // Seq(2, 4, 6, 8, 10)
```

### Filter

```scala
val seq = Seq(1, 2, 3, 4, 5)
val evens = seq.filter(_ % 2 == 0) // Seq(2, 4)
```

### FlatMap

```scala
val seq = Seq(1, 2, 3)
val flatMapped = seq.flatMap(x => Seq(x, x * 2)) // Seq(1, 2, 2, 4, 3, 6)
```

## Aggregation

### Fold and Reduce

```scala
val seq = Seq(1, 2, 3, 4, 5)

// Sum using fold
val sum = seq.fold(0)(_ + _) // 15

// Product using reduce
val product = seq.reduce(_ * _) // 120
```

### Finding Elements

```scala
val seq = Seq(1, 2, 3, 4, 5)

// Find first even number
val firstEven = seq.find(_ % 2 == 0) // Some(2)

// Check if any element satisfies a condition
val hasEven = seq.exists(_ % 2 == 0) // true

// Check if all elements satisfy a condition
val allPositive = seq.forall(_ > 0) // true
```

## Sorting and Ordering

```scala
val seq = Seq(3, 1, 4, 1, 5, 9, 2, 6)

// Sort in ascending order
val sorted = seq.sorted // Seq(1, 1, 2, 3, 4, 5, 6, 9)

// Sort in descending order
val descending = seq.sortWith(_ > _) // Seq(9, 6, 5, 4, 3, 2, 1, 1)

// Sort by a key
case class Person(name: String, age: Int)
val people = Seq(Person("Alice", 30), Person("Bob", 25), Person("Charlie", 35))
val sortedByAge = people.sortBy(_.age) // Seq(Person("Bob", 25), Person("Alice", 30), Person("Charlie", 35))
```

This cheatsheet covers some of the most common operations on Scala Seq. Remember that Seq is an immutable trait by default, so operations like `:+` and `++` return new sequences rather than modifying the original.
