**GreaterThanOrEqualConstraint** tests that one value is greater than or equal to another.

<h4>Constructor</h4>
```C#
GreaterThanOrEqualConstraint(object expected)
```

<h4>Syntax</h4>
```C#
Is.GreaterThanOrEqualTo(object expected)
Is.AtLeast(object expected)
```

<h4>Modifiers</h4>
```C#
...Using(IComparer comparer)
...Using<T>(IComparer&lt;T&gt; comparer)
...Using<T>(Comparison&lt;T&gt; comparer)
```

<h4>Examples of Use</h4>
```C#
Assert.That(7, Is.GreaterThanOrEqualTo(3));
Assert.That(7, Is.AtLeast(3));
Assert.That(7, Is.GreaterThanOrEqualTo(7));
Assert.That(7, Is.AtLeast(7));
Assert.That(myOwnObject, 
    Is.GreaterThanOrEqualTo(theExpected).Using(myComparer));
```

