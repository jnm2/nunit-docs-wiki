**RangeConstraint** tests that a value is in an (inclusive) range.

<h4>Constructor</h4>

```C#
RangeConstraint(IComparable from, IComparable to)
```

<h4>Syntax</h4>

```C#
Is.InRange(IComparable from, IComparable to)
```

<h4>Modifiers</h4>

```C#
...Using(IComparer comparer)
...Using<T>(IComparer<T> comparer)
...Using<T>(Comparison<T> comparer)
```

<h4>Examples of Use</h4>

```C#
int[] iarray = new int[] { 1, 2, 3 }

Assert.That( 42, Is.InRange(1, 100) );
Assert.That( iarray, Is.All.InRange(1, 3) );
Assert.That(myOwnObject, 
    Is.InRange(lowExpected, highExpected).Using(myComparer));
```
