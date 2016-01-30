**ExactCountConstraint** applies a constraint to each item in an `IEnumerable`, succeeding if the specified number of items succeed. An exception is thrown if the actual value passed does not implement `IEnumerable`.

<h4>Constructor</h4>

```C#
ExactCountConstraint(int expectedCount, Constraint itemConstraint)
```

<h4>Syntax</h4>

```C#
Has.Exactly(int expectedCount)...
```

<h4>Examples of Use</h4>

```C#
int[] array = new int[] { 1, 2, 3 };
Assert.That( array, Has.Exactly(1).EqualTo(3) );
Assert.That( array, Has.Exactly(2).GreaterThan(1) );
Assert.That( array, Has.Exactly(3).LessThan(100) );
```

