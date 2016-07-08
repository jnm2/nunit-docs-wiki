**CollectionEquivalentConstraint** tests that two `IEnumerables` are equivalent - that they contain
the same items, in any order. If the actual value passed does not implement `IEnumerable` an exception is thrown.

<h4>Constructor</h4>

```C#
CollectionEquivalentConstraint( IEnumerable other )
```

<h4>Syntax</h4>

```C#
Is.EquivalentTo( IEnumerable other )
```

<h4>Examples of Use</h4>

```C#
int[] iarray = new int[] { 1, 2, 3 };
string[] sarray = new string[] { "a", "b", "c" };
Assert.That( new string[] { "c", "a", "b" }, Is.EquivalentTo( sarray ) );
Assert.That( new int[] { 1, 2, 2 }, Is.Not.EquivalentTo( iarray ) );
```

<h4>Notes</h4>

1. To compare items in order, use Is.EqualTo().

