###DRAFT
NUnit 2.6 has a number of Asserts and Constraints that deal with files, directories and/or paths. There are a number of gaps and inconsistencies in this set of features. This specification attempts to more clearly define what each of them should do in NUnit 3.0.

### Existing Asserts and Constraints

The following table lists those Asserts and Constraints in NUnit 2.6, which deal with files,
directories or paths.

|      Classic Assert Form      |      Constraint Used       |      Assert.That Syntax        |
|-------------------------------|----------------------------|--------------------------------|
|  DirectoryAssert.AreEqual     |  EqualConstraint           |  Is.EqualTo(DirectoryInfo)     |
|  DirectoryAssert.AreNotEqual  |  EqualConstraint           |  Is.Not.EqualTo(DirectoryInfo) |
|  DirectoryAssert.IsEmpty      |  EmptyDirectoryConstraint  |  Is.Empty                      |
|  DirectoryAssert.IsNotEmpty   |  EmptyDirectoryConstraint  |  Is.Not.Empty                  |
|  DirectoryAssert.IsWithin     |  SubDirectoryConstraint    |  none                          |
|  DirectoryAssert.IsNotWithin  |  SubDirectoryConstraint    |  none                          |
|  FileAssert.AreEqual          |  EqualConstraint           |  Is.EqualTo(FileInfo)          |
|  FileAssert.AreNotEqual       |  EqualConstraint           |  Is.Not.EqualTo(FileInfo)      |
|  none                         |  SamePathConstraint        |  Is.SamePath(string)           |
|  none                         |  SamePathOrUnderConstraint |  Is.SamePathOrUnder(string)    |

#### Differences

One clear division is immediately visible. The operations of DirectoryAssert and FileAssert are not fully available using the constraint-based syntax, while the path operations are not available using any classic form. This is due to the fact that DirectoryAssert and FileAssert were contributed with code in the assert classes themselves and only later retrofitted to use newly developed constraints. To the extent (to be determined) that we continue to support these operations, a constraint-based syntax should be added.

On the other hand, PathConstraint was added after the release of the new syntactic model using constraints and there seems to be no need to add a more clasic form.

A second level of difference has to do with the semantics of the operations. Some operations require that the actual and expected directories or files actually exist and will fail or throw an exception if they do not. Others - in particular the path constraints - operate solely on the text of the paths. In this way, the asserts and constraints differ in the same way that the .NET methods of the Directory and File classes differ from those of the Path class. This difference is quite important when testing the value of a path to a file that has not yet been created. Specific details for each Constraint follow...

###### EqualConstraint

When used with a DirectoryInfo or FileInfo, the directories or files need not exist. However, in order to initially create a DirectoryInfo or FileInfo, a valid path is required. When used with a Stream, file contents are directly compared.

###### EmptyDirectoryConstraint

The directory must exist. If not an exception is thrown.

###### SubDirectoryConstraint

Both directories must exist. If not an exception is thrown.

###### SamePathConstraint

The file system is never accessed so the path does not have to exist or even be valid.

###### SamePathOrUnderConstraint

The file system is never accessed so the paths need not exist or even be valid.

### Planned Changes

#### DirectoryAssert

- [x] Mark DirectoryAssert Obsolete in the next NUnit 2.5 release and remove it from NUnit 3.0. (DirectoryAssert has been removed from NUnit 3.0)
Existing methods would be functionally replaced as follows:

###### AreEqual / AreNotEqual

- [x] Use Assert.AreEqual() or Assert.That(..., Is.EqualTo()) with DirectoryInfo arguments. The new [[Extended Constraint Syntax]] should handle this as well.

###### IsEmpty / IsNotEmpty

- [x] Extend Is.Empty syntax, which now works for strings and collections to also handle DirectoryInfos. Add support to the new [[Extended Constraint syntax]] to handle this.

###### IsWithin / IsNotWithin

- [x] Use existing Is.SamePath() syntax for strings and remove support for performing this operation on DirectoryInfos.

###### Directory Existence

- [x] Add a DirectoryExists constraint and provide extended syntax to access it. For example...
  Assert.That(dirInfo).Exists;

#### FileAssert

- [x] Continue to support FileAssert and add an Exists method. Investigate ways to support this using the new [[Extended Constraint Syntax]].

#### Path Constraints

- [x] Continue to support SamePathConstraint and SamePathOrUnderConstraint.

#### Status

All of the above Planned Changes are complete except for extending them to support the [[Extended Constraint Syntax]] because that project has not been started.

You can now write asserts like the following

```C#
Assert.That(fileStr, Does.Exist);
Assert.That(dirStr, Does.Exist);
Assert.That(fileStr, Does.Not.Exist);
Assert.That(new FileInfo(fileStr), Does.Exist);
Assert.That(new DirectoryInfo(dirStr), Does.Exist);
Assert.That(new DirectoryInfo(actual), Is.EqualTo(expected));

FileAssert.Exists(fileStr);
FileAssert.Exists(new FileInfo(fileStr));
FileAssert.DoesNotExist(fileStr);
FileAssert.DoesNotExist(new FileInfo(fileStr));

Assert.That(new DirectoryInfo(actual), Is.Empty);
Assert.That(new DirectoryInfo(actual), Is.Not.Empty);
```