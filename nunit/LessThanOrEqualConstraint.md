**LessThanOrEqualConstraint** tests that one value is less than or equal to another.

<h4>Constructor</h4>
```C#
LessThanOrEqualConstraint(object expected)
```

<h4>Syntax</h4>
```C#
Is.LessThanOrEqualTo(object expected)
Is.AtMost(object expected)
```

<h4>Modifiers</h4>
```C#
...Using(IComparer comparer)
...Using<T>(IComparer&lt;T&gt; comparer)
...Using<T>(Comparison&lt;T&gt; comparer)
```

<h4>Examples of Use</h4>
```C#
Assert.That(3, Is.LessThanOrEqualTo(7));
Assert.That(3, Is.AtMost(7));
Assert.That(3, Is.LessThanOrEqualTo(3));
Assert.That(3, Is.AtMost(3));
Assert.That(myOwnObject, 
    Is.LessThanOrEqualTo(theExpected).Using(myComparer));
```

