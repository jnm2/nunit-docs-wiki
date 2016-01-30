The **EmptyDirectoryConstraint** tests if a Directory is empty.

<h4>Constructor</h4>
```C#
EmptyDirectoryConstraint()
```

<h4>Syntax</h4>
```C#
Is.Empty
```

<h4>Examples of Use</h4>
```C#
Assert.That(new DirectoryInfo(actual), Is.Empty);
Assert.That(new DirectoryInfo(actual), Is.Not.Empty);
```

**Note:** `Is.Empty` actually creates an `EmptyConstraint`. Subsequently applying it to a `DirectoryInfo` causes an `EmptyDirectoryConstraint` to be created.