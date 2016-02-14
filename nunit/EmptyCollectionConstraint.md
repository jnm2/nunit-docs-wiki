The **EmptyCollectionConstraint** tests if a Collection or other `IEnumerable` is empty. An `ArgumentException` is thrown if the actual value is not an `IEnumerable` or is null. 

<h4>Constructor</h4>
```C#
EmptyCollectionConstraint()
```

<h4>Syntax</h4>
```C#
Is.Empty
```

<h4>Examples of Use</h4>
```C#
Assert.That(new int[] { }, Is.Empty);
Assert.That(new int[] { 1, 2, 3 }, Is.Not.Empty);
```

**Note:** `Is.Empty` actually creates an `EmptyConstraint`. Subsequently applying it to an `IEnumerable` or `ICollection` causes an `EmptyCollectionConstraint` to be created.