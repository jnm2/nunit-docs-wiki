**CollectionContainsConstraint** tests that an `IEnumerable` contains an object. If the actual value passed does not implement `IEnumerable`, an exception is thrown.

<h4>Constructor</h4>

```C#
CollectionContainsConstraint( object )
```

<h4>Syntax</h4>

```C#
Has.Member( object )
Contains.Item( object )
Does.Contain( object )
```

<h4>Modifiers</h4>

```C#
...Using(IComparer comparer)
...Using<T>(IComparer<T> comparer)
...Using<T>(Comparison<T> comparer)
```

<h4>Examples of Use</h4>

```C#
int[] iarray = new int[] { 1, 2, 3 };
string[] sarray = new string[] { "a", "b", "c" };
Assert.That( iarray, Has.Member(3) );
Assert.That( sarray, Has.Member("b") );
Assert.That( sarray, Contains.Item("c") );
Assert.That( sarray, Has.No.Member("x") );    
Assert.That( iarray, Does.Contain(3) );
```

<h4>Notes</h4>

1. For references, <b>Has.Member</b> uses object equality to find a member in a
   collection. To check for an object equal to an item the collection, use
   <b>Has.Some.EqualTo(...)</b>.

