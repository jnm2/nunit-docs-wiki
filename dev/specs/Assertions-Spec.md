### DRAFT
This page lists all Assertions to be supported by the NUnit 3.0 framework, including classic Asserts as well as constraints used in constraint-based assertions. Not all assertions are supported equally by the various framework distributions. See [[Assertion Support]] and [[Constraint Support]] for details of support.

### Existing (2.5) Features

The following tables list all asserts and constraints supported by NUnit 2.5. Unless otherwise noted, we plan to support them without change in NUnit 3.0. 

#### Asserts

| Feature  |  Status / Notes  |
|----------|------------------|
| Assert.Null/IsNull        | |
| Assert.NotNull/IsNotNull  | |
| Assert.True/IsTrue        | |
| Assert.False/IsFalse      | |
| Assert.Pass               | |
| Assert.Fail               | |
| Assert.Ignore             | |
| Assert.Inconclusive       | |
| Assert.That               | |
| Assert.Throws             | |
| Assert.Catch              | |
| Assert.IsNaN              | |
| Assert.IsEmpty            | |
| Assert.IsNotEmpty         | |
| Assert.IsNullOrEmpty      | |
| Assert.IsNotNullOrEmpty   | |
| Assert.IsAssignableFrom   | |
| Assert.IsNotAssignableFrom| |
| Assert.IsAssignableTo     | |
| Assert.IsNotAssignableTo  | |
| Assert.IsInstanceOf       | |
| Assert.IsNotInstanceOf    | |
| Assert.AreEqual           | |
| Assert.AreNotEqual        | |
| Assert.AreSame            | |
| Assert.AreNotSame         | |
| Assert.Greater            | |
| Assert.Less               | |
| Assert.GreaterOrEqual     | |
| Assert.LessOrEqual        | |
| Assert.Contains           | |
| StringAssert              | |
| CollectionAssert          | |
| FileAssert                | |
| DirectoryAssert           | May be eliminated. See the writeup on [[File, Directory and Path Assertions]] |

#### Constraints

| Feature  |  Status / Notes  |
|----------|------------------|
| AllItemsConstraint              | |
| AndConstraint                   | |
| AssignableFromConstraint        | |
| AssignableToConstraint          | |
| AttributeConstraint             | |
| AttributeExistsConstrant        | |
| BinarySerializableConstraint    | |
| CollectionContainsConstraint    | |
| CollectionEquivalentConstraint  | |
| CollectionOrderedConstraint     | |
| CollectionSubsetConstraint      | |
| ContainsConstraint              | |
| DelayedConstraint               | |
| EmptyCollectionConstraint       | |
| EmptyConstraint                 | |
| EmptyDirectoryConstraint        | |
| EmptyStringConstraint           | |
| EndsWithConstraint              | |
| EqualConstraint                 | |
| ExactTypeConstraint             | |
| FalseConstraint                 | |
| GreaterThanConstraint           | |
| GreaterThanOrEqualConstraint    | |
| InstanceOfTypeConstraint        | |
| LessThanConstraint              | |
| LessThanOrEqualConstraint       | |
| NaNConstraint                   | |
| NoItemConstraint                | |
| NotConstraint                   | |
| NullConstraint                  | |
| NullOrEmptyStringConstraint     | |
| OrConstraint                    | |
| PredicateConstraint             | |
| PropertyConstraint              | |
| PropertyExistsConstraint        | |
| RangeConstraint                 | |
| RegexConstraint                 | |
| SameAsConstraint                | |
| SamePathConstraint              | |
| SamePathOrUnderConstraint       | |
| SomeItemsConstraint             | |
| StartsWithConstraint            | |
| SubDirectoryConstraint          | |
| SubstringConstraint             | |
| ThrowsConstraint                | |
| ThrowsNothingConstraint         | |
| TrueConstraint                  | |
| UniqueItemsConstraint           | |
| XmlSerializableConstraint       | |

### New Featues

As new features are identified, they will be listed here.


