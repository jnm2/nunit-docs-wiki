**FileOrDirectoryExistsConstraint** tests that a File or Directory exists.

<h4>Constructor</h4>

```C#
FileOrDirectoryExistsConstraint()
```

<h4>Syntax</h4>

```C#
Does.Exist
Does.Not.Exist
```

<h4>Modifiers</h4>

```C#
IgnoreDirectories
IgnoreFiles
```

<h4>Examples of Use</h4>

```C#
Assert.That(fileStr, Does.Exist);
Assert.That(dirStr, Does.Exist);
Assert.That(fileStr, Does.Not.Exist);
Assert.That(dirStr, Does.Not.Exist);

Assert.That(new FileInfo(fileStr), Does.Exist);
Assert.That(new DirectoryInfo(dirStr), Does.Exist);
```
