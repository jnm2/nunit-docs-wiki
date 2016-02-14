The **EmptyStringConstraint** tests if a string is empty.

<h4>Constructor</h4>
```C#
EmptyStringConstraint()
```
 
<h4>Syntax</h4>
```C#
Is.Empty
```

<h4>Examples of Use</h4>
```C#
Assert.That(string.Empty, Is.Empty);
Assert.That("A String", Is.Not.Empty);
```

**Note:** `Is.Empty` actually creates an `EmptyConstraint`. Subsequently applying it to a `string` causes an `EmptyStringConstraint` to be created.