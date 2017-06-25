In NUnit 3, test execution is done using command objects, which are constructed for each test. Execution of a single test will  generally require multiple nested commands. Some attributes are able to contribute to the chain of commands. For example, `MaxTimeAttribute` adds a command, which examines the elapsed time to complete a test and fails it if a specified maximum was exceeded.

Attributes add to the command chain by and implementing the two interfaces that derive from the `ICommandWrapper` interface. The interfaces are defined as follows:

```C#
public interface ICommandWrapper
{
    TestCommand Wrap(TestCommand command);
}

public interface IWrapTestMethod : ICommandWrapper
{
}

public interface IWrapSetUpTearDown : ICommandWrapper
{
}
```

Attributes should __not__ implement the `ICommandWrapper` interface directly but should select one of the derived attributes. NUnit applies the `IWrapSetUpTearDown` interface before SetUp and after TearDown. It applies the `IWrapTestMethod` interface after SetUp and before the test is run.

The `Wrap` should return an appropriate command in which the original command has been nested. For an example, see the implementation of MaxTimeAttribute.
