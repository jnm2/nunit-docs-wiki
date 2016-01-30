**CollectionOrderedConstraint** tests that an `IEnumerable` is ordered. If the actual value passed does not implement `IEnumerable`, an exception is thrown.

<h4>Constructor</h4>

```C#
CollectionOrderedConstraint()
```

<h4>Syntax</h4>

```C#
Is.Ordered
```

<h4>Modifiers</h4>

```C#
...Descending
...By(string propertyName)
...Using(IComparer comparer)
...Using&lt;T&gt;(IComparer&lt;T&gt; comparer)
...Using&lt;T&gt;(Comparison&lt;T&gt; comparer)
```

<h4>Examples of Use</h4>

```C#
int[] iarray = new int[] { 1, 2, 3 };
string[] sarray = new string[] { "c", "b", "a" };
string[] sarray2 = new string[] ( "a", "aa", "aaa" );
Assert.That( iarray, Is.Ordered );
Assert.That( sarray, Is.Ordered.Descending );
Assert.That( sarray2, Is.Ordered.By("Length");
```

<h4>Notes</h4>

1. Modifiers may be combined and may appear in any order. If the
   same modifier is used more than once, the result is undefined.
