This feature enables the test developer to put reusable test logic into attributes and attach this logic to assemblies, classes, interfaces and methods. The reusable test logic is then run before and after test suites and test cases execute. It enables the test developer to build smaller bits of reusable test logic and to compose them in unique ways as is needed.  

### Benefits

This feature provides three main benefits:

  * it enables the development of reusable test code without creating large, coupled, cumbersome base test fixtures with common test logic.
  * it improves comprehension of test code because a simple attribute name can summarize what the reusable test logic does. 
  * it provides an easy way to distribute such extended logic for use by others, by encapsulating it in a single attribute.

### Design

Attributes are ideal to imbed reusable test logic into because attributes can be applied at various locations within .NET code: at an assembly level, at a type (e.g. class, struct, interface) level, or at a member (e.g. method, property, field) level.  NUnit interprets classes and methods as test suites and test cases.  For example, NUnit interprets classes with the TestFixture attribute applied as a test suite.  Each test method within the class are interpreted as a test case.  However, there are times when a method is interpreted as a test suite, for example, when one or more TestCase attribute is attached to the method and the method has some arguments.  In that case, the class is interpreted as a test suite that has a child test suite represented by the method, and that child test suite contains a test case for each TestCase attribute applied to the method.  The importance of understanding this will become apparent when you are trying to determine when the reusable test logic in attributes will execute during the execution of test suites and test cases.

Any attribute can be an action attribute.  To create an action attribute, create a class that inherits from System.Attribute and implements the ITestAction interface. Alternatively, you may inherit from NUnit's TestActionAttribute, which provides a default
implemenation of the interface that you can override. The interface and associated Types are defined as follows:

```csharp
[Flags]
public enum ActionTargets
{
    Default = 0,

    Test = 1,

    Suite = 2
}

public class TestDetails
{
    ...
    
    public object Fixture { get; private set; }
    
    public MethodInfo Method { get; private set; }
    
    public string FullName { get; private set; }
    
    public string Type { get; private set; }
    
    public bool IsSuite { get; private set;' }
}

public interface ITestAction
{
    void BeforeTest(TestDetails details);

    void AfterTest(TestDetails details);

    ActionTargets Targets { get; }
}
```

The value returned from the Targets property determines when the BeforeTest and AfterTest methods will be called.

When an attribute that returns ActionTargets.Suite is applied to either a class or a parameterized method, NUnit will execute the attribute's BeforeTest method prior to executing the test suite and then execute the AfterTest method after the test suite has finished executing. This is similar to how the TestFixtureSetUp and TestFixtureTearDown attributes work.

On the other hand, when an attribute that returns ActionTargets.Test is used in the same situations, NUnit will execute the attribute's BeforeTest method prior to each contained test case and the AfterTest method after each test case. This is similar to how the SetUp and TearDown attributes work.

Action attributes that return ActionTargets.Default target the particular code item to which they are attached. When attached to a method, they behave as if ActionTargets.Test had been specified. When attached to a class or assembly, they behave as if ActionTargets.Suite was returned.

### Usage

The general idea with Action Attributes is to better enable
composability. Often when writing unit tests we have logic
that we want to run upon certain events in the test cycle (e.g.
SetUp, TearDown, FixtureSetUp, FixtureTearDown, etc.). As we discussed above,
NUnit has had the ability to execute code upon these events by
decorating fixture classes and methods with the appropriate NUnit-
provided attributes.  The difference between what NUnit already offers
and what Action Attributes offer is composability.

Suppose we have some tests in multiple fixtures that need the same in-
memory test database to be created and destroy on each test run.  We
could create a base fixture class and then my fixtures that depend on
the test database could simply inherit from that base fixture class.
That works fine, until we need some other reusable functionality, say
the ability to configure or reset a ServiceLocator.  We could put that
functionality in the same base fixture class, but now we're mixing two
different responsibilities into the base class.  In some cases we may
*not* want the test database, but we do want ServiceLocator
configuration; and sometimes we want the opposite.  Still other times
we'll want both - so we'd have to make the base class configurable.

Now what happens when we discover a third piece of functionality we need
to reuse, for example, configuring the Thread's CurrentPrincipal in arbitrary
ways - we could add that to my base class, but the complexity of the
base class grows very quickly.  We've violated the Single
Responsibility Principle and suffering for it.  What we really want is
the ability to separate the different pieces of resuable test logic and compose
them together as our tests need them.

Given this example:

```csharp
[TestFixture, ResetServiceLocator]
public class MyTests
{
 [CreateTestDatabase]
 public void Test1() { /* ... */ }

 [CreateTestDatabase, AsAdministratorPrincipal]
 public void Test2() { /* ... */ }

 [CreateTestDatabase, AsNamedPrincipal("charlie.poole")]
 public void Test3() { /* ... */ }

 [AsGuestPrincipal]
 public void Test4() { /* ... */ }
}
```

We've identified five different actions
(ResetServiceLocator, CreateTestDatabase, AsAdministratorPrincipal,
AsNamedPrincipal, AsGuestPrincipal) that we want to compose together in
different ways for different tests.  We could reuse these actions in
other test fixtures, without having to inherit from a base class.  We could 
even develop a library of common test actions that we could distribute.

Now, we could develop a base class that has a empty collection of
behaviors, and any class that derives from it could add behaviors to
the collection in the constructor.  However, this still uses up the
precious *one* base class that our test fixture could inherit from.
By using Action Attributes, we can reserve inheriting from a base class
for some other purpose.

### Examples

For the next few example we will use the following sample Action Attribute:

```csharp
[AttributeUsage(AttributeTargets.Method | AttributeTargets.Class |
                AttributeTargets.Interface | AttributeTargets.Assembly,
                AllowMultiple = true)]
public class ConsoleActionAttribute : Attribute, ITestAction
{
    private string _Message;

    public ConsoleActionAttribute(string message) { _Message = message; }

    public void BeforeTest(TestDetails details)
    {
        WriteToConsole("Before", details);
    }

    public void AfterTest(TestDetails details)
    {
        WriteToConsole("After", details);
    }
    
    public ActionTargets Targets
    {
        get { return ActionTargets.Test | ActionTargets.Suite; }
    }

    private void WriteToConsole(string eventMessage, TestDetails details)
    {
        Console.WriteLine("{0} {1}: {2}, from {3}.{4}.",
            eventMessage,
            details.IsSuite ? "Suite" : "Case",
            _Message,
            details.Fixture != null ? details.Fixture.GetType().Name : "{no fixture}",
            details.Method != null ? details.Method.Name : "{no method}");
    }
}
```

Note that the above Action Attribute returns the union of ActionTargets.Test and ActionTargets.Suite. This is permitted, but will probably not be the normal case. It is done here so we can reuse the attribute in multiple examples. The attribute takes a single constructor argument, a message, that will be used to write output to the console. All of the Before and After methods write output via the WriteToConsole method. 

#### Method Attached Actions

##### Example 1 (applied to simple test method):

```csharp
[TestFixture]
public class ActionAttributeSampleTests
{
    [Test][ConsoleAction("Hello")]
    public void SimpleTest()
    {
        Console.WriteLine("Test ran.");
    }
}
```

###### Console Output:

  Before Case: Hello, from ActionAttributeSampleTests.SimpleTest.
  Test ran.
  After Case: Hello, from ActionAttributeSampleTests.SimpleTest.

##### Example 2 (applied action twice to test method):

```csharp
[TestFixture]
public class ActionAttributeSampleTests
{
    [Test] [ConsoleAction("Hello")]
    [ConsoleAction("Greetings")]
    public void SimpleTest()
    {
        Console.WriteLine("Test run.");
    }
}
```

###### Console Output:

  Before Case: Greetings, from ActionAttributeSampleTests.SimpleTest.
  Before Case: Hello, from ActionAttributeSampleTests.SimpleTest.
  Test run.
  After Case: Hello, from ActionAttributeSampleTests.SimpleTest.
  After Case: Greetings, from ActionAttributeSampleTests.SimpleTest.
  
###### Remarks
You are permitted to apply the same attribute multiple times.

##### Example 3 (applied to a test method with test cases):

```csharp
[TestFixture]
public class ActionAttributeSampleTests
{
    [Test] [ConsoleAction("Hello")]
    [TestCase("02")]
    [TestCase("01")]
    public void SimpleTest(string number)
    {
        Console.WriteLine("Test run {0}.", number);
    }
}
```

###### Console Output:

  Before Suite: Hello, from ActionAttributeSampleTests.SimpleTest.
  Before Case: Hello, from ActionAttributeSampleTests.SimpleTest.
  Test run 01.
  After Case: Hello, from ActionAttributeSampleTests.SimpleTest.
  Before Case: Hello, from ActionAttributeSampleTests.SimpleTest.
  Test run 02.
  After Case: Hello, from ActionAttributeSampleTests.SimpleTest.
  After Suite: Hello, from ActionAttributeSampleTests.SimpleTest.

###### Remarks
When one or more [TestCase] attributes are applied to a method, NUnit treats the method as a test suite.  You'll notice that BeforeTestSuite was run once before both of the test cases, and AfterTestSuite was run once after both of the test cases.  BeforeTestCase and AfterTestCase is run for each test case.

#### Type Attached Actions

##### Example 1:

```csharp
[TestFixture] [ConsoleAction("Hello")]
public class ActionAttributeSampleTests
{
    [Test]
    public void SimpleTestOne()
    {
        Console.WriteLine("Test One.");
    }
    
    [Test]
    public void SimpleTestTwo()
    {
        Console.WriteLine("Test Two.");
    }
}
```

###### Console Output:

  Before Suite: Hello, from ActionAttributeSampleTests.{no method}.
  Before Case: Hello, from ActionAttributeSampleTests.SimpleTestOne.
  Test ran.
  After Case: Hello, from ActionAttributeSampleTests.SimpleTestOne.
  Before Case: Hello, from ActionAttributeSampleTests.SimpleTestTwo.
  Test ran.
  After Case: Hello, from ActionAttributeSampleTests.SimpleTestTwo.
  After Suite: Hello, from ActionAttributeSampleTests.{no method}.

###### Remarks
In this case, the class is the test suite. BeforeTestSuite and AfterTestSuite are run only once for this class.  BeforeTestCase and AfterTestCase are run for each test.

##### Example 2 (attached to interface):

```csharp
[ConsoleAction("Hello")]
public interface IHaveAnAction
{
}

[TestFixture]
public class ActionAttributeSampleTests : IHaveAnAction
{
    [Test] 
    public void SimpleTest()
    {
        Console.WriteLine("Test run.");
    }
}
```

###### Console Output:

  Before Suite: Hello, from ActionAttributeSampleTests.{no method}.
  Before Case: Hello, from ActionAttributeSampleTests.SimpleTest.
  Test run.
  After Case: Hello, from ActionAttributeSampleTests.SimpleTest.
  After Suite: Hello, from ActionAttributeSampleTests.{no method}.

###### Remarks
Action attributes can be applied to an interface.  If a class marked with [TestFixture] implements an interface that has an action attribute applied to the interface, the class inherits the action attribute from the interface.  It behaves as if you applied the action attribute to the class itself.

##### Example 3 (action attribute is applied to interface and attribute uses interface to provide data to tests):

```csharp
[AttributeUsage(AttributeTargets.Interface)]
public class InterfaceAwareActionAttribute : Attribute, ITestCaseAction
{
    private readonly string _Message;
    public InterfaceAwareActionAttribute(string message) { _Message = message; }

    public void BeforeTestCase(object fixture, MethodInfo method)
    {
        IHaveAnAction obj = fixture as IHaveAnAction;
        if(obj != null)
            obj.Message = _Message;
    }

    public void AfterTestCase(object fixture, MethodInfo method) { }
}

[InterfaceAwareAction("Hello")]
public interface IHaveAnAction { string Message { get; set; } }

[TestFixture]
public class ActionAttributeSampleTests : IHaveAnAction
{
    [Test] 
    public void SimpleTest()
    {
        Console.WriteLine("{0}, World!", Message);
    }

    public string Message { get; set; }
}
```

###### Console Output:

  Hello, World!

###### Remarks

Here we see a new action attribute, [InterfaceAwareAction].  This attribute uses the fixture argument passed into BeforeTestCase and casts it to an interface, IHaveAnAction.  If the fixture implements the IHaveAnAction interface, the attribute sets the Message property to the string passed into the constructor of the attribute.  Since the attribute is applied to the interface, any class that implements this interface gets it's Message property set to the string provided to the constructor of the attribute.  This is useful when the action attribute provides some data or service to the tests.

#### Assembly Attached Action

##### Example 1:

```csharp
[assembly: ConsoleAction("Hello")]

[TestFixture]
public class ActionAttributeSampleTests
{
    [Test] 
    public void SimpleTest()
    {
        Console.WriteLine("Test run.");
    }
}
```

###### Console Output:

  Before Suite: Hello, from {no fixture}.{no method}.
  Before Case: Hello, from ActionAttributeSampleTests.SimpleTest.
  Test run.
  After Case: Hello, from ActionAttributeSampleTests.SimpleTest.
  After Suite: Hello, from {no fixture}.{no method}.

###### Remarks

The [ConsoleAction] attribute in this example is applied to the entire assembly.  NUnit treats an assembly as a test suite (in fact, a suite of suites).  Since the [ConsoleAction] attribute implements both ITestSuiteAction and ITestCaseAction, NUnit will run BeforeTestSuite once before any tests are run in the assembly, and AfterTestSuite after all tests are run in the assembly.  Additionally, BeforeTestCase and AfterTestCase will be run for every test case in the assembly.  It is unlikely that action attributes are applied to assemblies often.  However, it is useful to build action attributes that ensure state gets cleaned up before and after each tests to prevent individual tests from affecting the outcome of other test.  For example, if you have any static or cached data or services, an action attribute can be used to clean them up for each test.