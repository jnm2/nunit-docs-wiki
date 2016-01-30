**EmptyConstraint** tests that an object is an empty string, directory or collection.

<h4>Constructor</h4>
```C#
EmptyConstraint()
```

<h4>Syntax</h4>
```C#
Is.Empty
```

<h4>Examples of Use</h4>
```C#
Assert.That( aString, Is.Empty );
Assert.Thst( dirInfo, Is.Empty );
Assert.That( collection, Is.Empty );
```

<h4>Notes</h4>
<ol>
<li><b>EmptyConstraint</b> creates and uses either an [[EmptyStringConstraint]],
[[EmptyDirectoryConstraint]] or [[EmptyCollectionConstraint]] depending on 
the argument tested.
<li>A `DirectoryInfo` argument is required in order to test for an empty directory.
To test whether a string represents a directory path, you must first construct
a <b>DirectoryInfo</b>.
</ol>

