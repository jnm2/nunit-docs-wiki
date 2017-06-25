### OUT OF DATE - UPDATE IN PROCESS

NUnit 3.0 implements a great deal of its functionality in its attributes. This functionality is accessed through a number of standard interfaces, which are implemented by the attributes. Users may create their own attributes by implementing these interfaces. 

For ease of understanding, the interfaces are grouped according to the stage in the life-cycle of a test at which they are used. The two primary stages in the life of a test are Load-Time and Execution-Time.

### Load-Time Interfaces

_Loading_ tests means loading the assembly into memory and examining its content to discover the classes and fixtures that represent tests. The internal structures that represent tests are built at this time. If requested by the application, information about the tests may be returned for display, as is done in the NUnit GUI runner.

The following interfaces are called at load time.

| Interface              | Used By |
|------------------------|---------|
| [[IFixtureBuilder|IFixtureBuilder-Interface]]       | Attributes that know how to build a fixture from a test class
| [[ITestBuilder|ITestBuilder-Interface]]              | Attributes that know how to build one or more parameterized test cases for a method
| [[ISimpleTestBuilder|ISimpleTestBuilder-Interface]] | Attributes that know how to build a single non-parameterized test case for a method
| [[IImplyFixture|IImplyFixture-Interface]]           | Attributes used on a method to signal that the defining class should be treated as a fixture
| [[IApplyToTest|IApplyToTest-Interface]]             | Attributes that make modifications to a test immediately after it is constructed

### Execution-Time Interfaces

At execution-time, some or all of the tests that were previously loaded are actually run. Their results are returned and made available to the application.

The following interfaces are called at execution time.

| Interface              | Used By |
|------------------------|---------|
| [[IApplyToContext|IApplyToContext-Interface | Attributes that set up the context prior to execution
| [[ICommandDecoratorSource]]
| [[ICommandDecorator]]

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
