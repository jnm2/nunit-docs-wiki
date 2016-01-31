**CollectionSupersetConstraint** tests that one `IEnumerable` is a superset of another. If the actual value passed does not implement `IEnumerable`, an exception is thrown.

<h4>Constructor</h4>

```C#
CollectionSupersetConstraint( IEnumerable )
```

<h4>Syntax</h4>

```C#
Is.SupersetOf( IEnumerable )
```

<h4>Example of Use</h4>

```C#
int[] iarray = new int[] { 1, 2, 3 };
Assert.That( iarray, Is.SupersetOf( new int[] { 1, 3 }) );
```

