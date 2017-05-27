**LessThanConstraint** tests that one value is less than another.

<h4>Constructor</h4>

```C#
LessThanConstraint(object expected)
```

<h4>Syntax</h4>

```C#
Is.LessThan(object expected)
Is.Negative // Equivalent to Is.LessThan(0)
```

<h4>Modifiers</h4>

```C#
...Using(IComparer comparer)
...Using<T>(IComparer<T> comparer)
...Using<T>(Comparison<T> comparer)
```

<h4>Examples of Use</h4>

```C#
Assert.That(3, Is.LessThan(7));
Assert.That(myOwnObject, 
    Is.LessThan(theExpected).Using(myComparer));
Assert.That(-5, Is.Negative);
```

