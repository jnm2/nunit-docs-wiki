**CollectionSubsetConstraint** tests that one `IEnumerable` is a subset of another. If the actual value passed does not implement `IEnumerable`, an exception is thrown.

<h4>Constructor</h4>

```C#
CollectionSubsetConstraint( IEnumerable )
```

<h4>Syntax</h4>

```C#
Is.SubsetOf( IEnumerable )
```

<h4>Example of Use</h4>

```C#
int[] iarray = new int[] { 1, 3 };
Assert.That( iarray, Is.SubsetOf( new int[] { 1, 2, 3 }) );
```

