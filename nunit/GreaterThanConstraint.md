**GreaterThanConstraint** tests that one value is greater than another.

<h4>Constructor</h4>

```C#
GreaterThanConstraint(object expected)
```

<h4>Syntax</h4>

```C#
Is.GreaterThan(object expected)
Is.Positive // Equivalent to Is.GreaterThan(0)
```

<h4>Modifiers</h4>

```C#
...Using(IComparer comparer)
...Using<T>(IComparer<T> comparer)
...Using<T>(Comparison<T> comparer)
```

<h4>Examples of Use</h4>

```C#
Assert.That(7, Is.GreaterThan(3));
Assert.That(myOwnObject, 
    Is.GreaterThan(theExpected).Using(myComparer));
Assert.That(42, Is.Positive);
```

