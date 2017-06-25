
#### ICommandDecoratorSource

In NUnit 2.x, tests were self-executing objects. In NUnit 3.0, execution is done using command objects, which are constructed for each test. Execution of a single test will  generally require multiple nested commands. Some attributes are able to contribute to the chain of commands. For example, `MaxTimeAttribute` adds a command, which examines the elapsed time to complete a test and fails it if a specified maximum was exceeded.

Attributes add to the command chain by creating a command decorator and implementing the `ICommandDecoratorSource` interface. The interface is defined as follows:

```C#
public interface ICommandDecoratorSource
{
    IEnumerable<ICommandDecorator> GetDecorators(MethodInfo method);
}
```

Custom attributes that require participation in the command chain may create and return a decorator. Note that the decorators returned may vary according to the state of the attribute and that returning an empty collection is valid.

#### ICommandDecorator

This interface is implemented by command decorators, which are normally separate objects from the attributes. The `ICommandDecorator` interface is defined as follows:

```C#
public interface ICommandDecorator
{
    CommandStage Stage { get; }
    int Priority { get; }
    TestCommand Decorate(TestCommand command);
}
```

There are various stages of command execution. In the current version of NUnit, the following stages are used:

```C#
public enum CommandStage
{
    Default,
    BelowSetUpTearDown, // Command runs after setup and cleans up before teardown
    SetUpTearDown,
    AboveSetUpTearDown  // Command runs before setup and cleans up after teardown
}
```

This is a preliminary definition, subject to change.

The int value of priority is used to set the order of execution within a single stage. It usually defaults to zero.

The Decorate method should return an appropriate command in which the original command has been nested. For examples, see the implementation of MaxTimeAttribute and ExpectedExceptionAttribute.
