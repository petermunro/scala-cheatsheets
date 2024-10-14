# Scala Map Operations Cheatsheet

Map in Scala is an immutable key-value data structure. Here's a cheatsheet of common Map operations with examples:

## Creating Maps

```scala
// Create a Map with specified key-value pairs
val scores = Map("Alice" -> 95, "Bob" -> 80, "Charlie" -> 90)

// Create an empty Map
val empty = Map.empty[String, Int]

// Create a Map from tuples
val tupleMap = Map(("A", 1), ("B", 2), ("C", 3))

// Create a Map using a builder
val builderMap = scala.collection.mutable.Map("X" -> 10, "Y" -> 20).toMap
```

## Accessing Elements

```scala
val scores = Map("Alice" -> 95, "Bob" -> 80, "Charlie" -> 90)

// Access by key (throws exception if key not found)
val aliceScore = scores("Alice") // 95

// Safe access with get (returns Option)
val bobScore = scores.get("Bob") // Some(80)

// Access with default value
val davidScore = scores.getOrElse("David", 0) // 0

// Check if key exists
val hasAlice = scores.contains("Alice") // true

// Get all keys
val allNames = scores.keys // Set("Alice", "Bob", "Charlie")

// Get all values
val allScores = scores.values // Iterable(95, 80, 90)
```

## Adding and Updating Elements

```scala
val scores = Map("Alice" -> 95, "Bob" -> 80)

// Add a new key-value pair
val updatedScores = scores + ("Charlie" -> 90) // Map("Alice" -> 95, "Bob" -> 80, "Charlie" -> 90)

// Update an existing key
val bobUpdated = scores + ("Bob" -> 85) // Map("Alice" -> 95, "Bob" -> 85)

// Add multiple pairs
val multipleAdded = scores ++ Map("Charlie" -> 90, "David" -> 85)

// Remove a key-value pair
val withoutBob = scores - "Bob" // Map("Alice" -> 95)

// Remove multiple keys
val withoutMultiple = scores -- List("Alice", "Bob") // Map()
```

## Transforming Maps

```scala
val scores = Map("Alice" -> 95, "Bob" -> 80, "Charlie" -> 90)

// Map: transform values
val percentages = scores.map { case (name, score) => (name, s"${score}%") }
// Map("Alice" -> "95%", "Bob" -> "80%", "Charlie" -> "90%")

// MapValues: transform only the values
val increased = scores.view.mapValues(_ + 5).toMap
// Map("Alice" -> 100, "Bob" -> 85, "Charlie" -> 95)

// Filter: keep entries that satisfy a predicate
val highScores = scores.filter { case (_, score) => score >= 90 }
// Map("Alice" -> 95, "Charlie" -> 90)

// Group by a function of the key-value pairs
val groupedByGrade = scores.groupBy { case (_, score) => 
  if (score >= 90) "A" else if (score >= 80) "B" else "C"
}
// Map("A" -> Map("Alice" -> 95, "Charlie" -> 90), "B" -> Map("Bob" -> 80))
```

## Merging Maps

```scala
val map1 = Map("A" -> 1, "B" -> 2)
val map2 = Map("B" -> 3, "C" -> 4)

// Merge with right bias (values from map2 override map1)
val merged = map1 ++ map2 // Map("A" -> 1, "B" -> 3, "C" -> 4)

// Merge with custom combination function
val customMerged = map1.merged(map2)(_ + _) // Map("A" -> 1, "B" -> 5, "C" -> 4)
```

## Aggregation and Folding

```scala
val scores = Map("Alice" -> 95, "Bob" -> 80, "Charlie" -> 90)

// Sum of all values
val totalScore = scores.values.sum // 265

// Fold
val scoreList = scores.foldLeft(List.empty[String]) { case (acc, (name, score)) =>
  s"$name: $score" :: acc
} // List("Charlie: 90", "Bob: 80", "Alice: 95")

// Reduce
val highest = scores.reduce((a, b) => if (a._2 > b._2) a else b) // ("Alice", 95)
```

## Searching and Filtering

```scala
val scores = Map("Alice" -> 95, "Bob" -> 80, "Charlie" -> 90)

// Find entry satisfying a predicate
val found = scores.find { case (_, score) => score > 85 } // Some(("Alice", 95))

// Check if any entry satisfies a predicate
val hasHigh = scores.exists { case (_, score) => score > 90 } // true

// Check if all entries satisfy a predicate
val allPassed = scores.forall { case (_, score) => score >= 70 } // true

// Count entries satisfying a predicate
val highScoreCount = scores.count { case (_, score) => score >= 90 } // 2
```

## Sorting

```scala
val scores = Map("Alice" -> 95, "Bob" -> 80, "Charlie" -> 90)

// Sort by keys
val sortedByName = scala.collection.immutable.SortedMap("Alice" -> 95, "Bob" -> 80, "Charlie" -> 90)

// Sort by values
val sortedByScore = scores.toList.sortBy(_._2).reverse.toMap
// LinkedHashMap("Alice" -> 95, "Charlie" -> 90, "Bob" -> 80)
```

## Conversion

```scala
val scores = Map("Alice" -> 95, "Bob" -> 80, "Charlie" -> 90)

// Convert to List of tuples
val list = scores.toList // List(("Alice", 95), ("Bob", 80), ("Charlie", 90))

// Convert to Set of tuples
val set = scores.toSet // Set(("Alice", 95), ("Bob", 80), ("Charlie", 90))

// Convert keys to List
val names = scores.keys.toList // List("Alice", "Bob", "Charlie")

// Convert values to Vector
val scoresVector = scores.values.toVector // Vector(95, 80, 90)
```

Remember that the default Map in Scala is immutable. Operations like `+` and `++` return new Maps rather than modifying the original. For mutable operations, you can use `scala.collection.mutable.Map`.
