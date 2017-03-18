### OUT OF DATE - UPDATE IN PROCESS

NUnit 3.0 implements a great deal of its functionality in its attributes. This functionality is accessed through a number of standard interfaces, which are implemented by the attributes. This technical note describes the interfaces used on NUnit attributes and recognized by NUnit when loading or running tests.

For ease of understanding, the interfaces are grouped according to the stage in the life-cycle of a test at which they are used. The two primary stages in the life of a test are Load-Time and Execution-Time.

### Load-Time Interfaces

_Loading_ tests means loading the assembly into memory and examining its content to discover the classes and fixtures that represent tests. The internal structures that represent tests are built at this time. If requested by the application, information about the tests may be returned for display, as is done in the NUnit GUI runner.

#### IFixtureBuilder

This interface is used by attributes that know how to build a fixture from a user class. `IFixtureBuilder` is defined as follows:

```C#
public interface IFixtureBuilder
{
    TestSuite BuildFrom(Type type);
}
```

Custom fixture builders should examine the provided Type and return an appropriate TestFixture based on it. If the fixture is intended to be an NUnit TestFixture, then the helper class `NUnitTestFixtureBuilder` may be used to create it.

The following NUnit attributes currently implement this interface:
* `TestFixtureAttribute`
* `SetUpFixtureAttribute`

> It would make more sense for this interface method to return `TestFixture` rather than `TestSuite`. We use `TestSuite` because it is the common base for both `TestFixture` and `SetupFixture`. In a future version, we will try to adjust the hierarchy so that all suites based on a class are derived from `TestFixture`.

#### ITestBuilder

This interface is used by attributes that know how to build one or more parameterized `TestMethod` instances from a `MethodInfo`. `ITestMethodBuilder` is defined as follows:

```C#
public interface ITestBuilder
{
    IEnumerable<TestMethod> BuildFrom(MethodInfo method, Test suite);
}
```

Custom attributes implementing this interface should examine the MethodInfo and return as many `TestMethod` instances as it is able to construct, using the parameters available to it. Some attributes will only return a single test, just as `TestCaseAttribute` does. Others, working like `TheoryAttribute` may return multiple tests. If no data is available to create tests, an empty collection should be returned. 

If the returned tests are standard NUnit TestMethods, the helper class `NUnitTestCaseBuilder` may be used to create them. 

The following NUnit attributes currently implement `ITestBuilder`:
* `CombiningStrategyAttribute`, with the following derived classes:
  * `CombinatorialAttribute`
  * `PairwiseAttribute`
  * `SequentialAttribute`
* `TestCaseAttribute`
* `TestCaseSourceAttribute`
* `TheoryAttribute`

#### ISimpleTestBuilder

This interface is used by attributes that know how to build a single, non-parameterized test from a `MethodInfo`. `ISimpleTestBuilder` is defined as follows:

```C#
public interface ISimpleTestBuilder
{
    TestMethod BuildFrom(MethodInfo method, Test suite);
}
```

Custom attributes implementing `ISimpleTestFixture` should examine the MethodInfo provided and return a single `TestMethod` instance, as appropriate to that method. The BuildFrom method should never return null, even if the specified method is not valid for a test. In that case, it should return a `TestMethod` with a RunState of NonRunnable, in order to provide feedback to the user who placed the attribute on the method.

NUnit treats attributes implementing this interface specially. They are ignored if any other attributes are present that implement `ITestBuilder`. This allows, for example, use of `[Test]` on a method that also has `[Combinatorial]` specified, without any error arising. Such usage has existed in NUnit for some time and this special handling of the interface allows us to preserve it.

In the current build, only `TestAttribute` implements this interface.

#### IImplyFixture

The `IImplyFixture` interface is an empty interface, used solely as a marker:

```C#
public interface IImplyFixture
{
}
```

If a class contains any method with an attribute that implements this interface, that class is treated as an NUnit TestFixture without any `TestFixture` attribute being specified. The following NUnit attributes currently implement this interface:
* `TestAttribute`
* `TestCaseAttribute`
* `TestCaseSourceAttribute`
* `TheoryAttribute`

#### IApplyToTest

The `IApplyToTest` interface is used to make modifications to a test immediately after it is constructed. It is defined as follows:

```C#
public interface IApplyToTest
{
    void ApplyToTest(Test test);
}
```

The `Test` Type is quite general and the argument may represent a suite or an individual test case. If the distinction is important, then you must code the attribute to examine the argument and react accordingly.

The interface may appear on the same attribute that is used to construct the test or on a separate attribute. In either case, it will only be called after the test is built. 

The order in which `ApplyToTest` is called on multiple attributes is indeterminate. If two attributes make completely independent changes to a test, then the order is not relevant. But if they both change the same property, or related properties, then it may necessary to make tests in the attribute code to ensure that the correct value 'wins'.

The most common example of this is for attributes that change the RunState of a test. If one attribute is trying to set it to `RunState.Ignore`, while the other wants it to be `RunState.NotRunnable`, we would normally expect the 'worst' value to win and for the test to be non-runnable. We can achieve that by code like the following:

```C#
// In the attribute setting NotRunable
test.RunState = RunState.NotRunnable;
...

// In the attribute setting Ignore
if (test.RunState != RunState.NotRunnable)
    test.RunState = RunState.Ignore;
```

The following NUnit attributes implement `IApplyToTest`:
* `CategoryAttribute`
* `CombiningStrategyAttribute`
* `CultureAttribute`
* `ExplicitAttribute`
* `IgnoreAttribute`
* `PlatformAttribute`
* `PropertyAttribute` (and, through it, a large number of derived attributes)
* `RequiresThreadAttribute`
* `TestAttribute`
* `TestFixtureAttribute`

### Execution-Time Interfaces

At execution-time, some or all of the tests that were previously loaded are actually run. Their results are returned and made available to the application.

#### IApplyToContext

NUnit tests run within a context, known as the `TestExecutionContext`. The context for a test case is nested within the context for its containing suite and so on, up to the assembly level. Attributes that implement `IApplyToContext` are called immediately after the context is created and before the test is run in order to make changes to the context. Once the test execution has completed, the context is discarded so that - effectively - any changes are reverted to their original values.

The `IApplyToContext` interface is defined as follows:
```C#
public interface IApplyToContext
{
    void ApplyToContext(TestExecutionContext context);
}
```

An example of the use of the context may be helpful. One item in the `TestExecutionContext` is the default timeout value for test cases. When any test is marked with `[Timeout(nnn)]` the context value is replaced by the supplied argument. The new timeout applies for any test case it appears on and any test case that is contained in a suite that it appears on. When the test or suite completes, the new value is discarded and the value contained in the original context is once against used.

Custom attributes that implement `IApplyToContext` should modify the TestExecutionContext in accordance with the arguments supplied to them. They are not called after the test is run and have no cleanup to perform.

The NUnit attributes that implement `IApplyToContext` are as follows:
* `ParallelizableAttribute`
* `SetCultureAttribute`
* `SetUICultureAttribute`
* `TimeoutAttribute`

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
