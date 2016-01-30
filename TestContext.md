Each NUnit test runs in an execution context, which includes information about the environment as well as the test itself. The `TestContext` class allows tests to access certain information about the execution context.

###Static Properties

####CurrentContext

Gets the context of the currently executing test. This context
is created separately for each test before it begins execution.
See below for properties of the current context.

####Out

Gets a TextWriter used for sending output to the current test result.

###Static Methods

```C#
    Write(bool value)
    Write(char value)
    Write(char[] value)
    Write(double value)
    Write(Int32 value)
    Write(Int64 value)
    Write(decimal value)
    Write(object value)
    Write(Single value)
    Write(string value)
    Write(UInt32 value)
    Write(UInt64 value)
    Write(string format, object arg1)
    Write(string format, object arg1, object arg2)
    Write(string format, object arg1, object arg2, object arg3)
    Write(string format, params object[] args)
```

Writes text to the current test result.

```C#
    WriteLine()
    WriteLine(bool value)
    WriteLine(char value)
    WriteLine(char[] value)
    WriteLine(double value)
    WriteLine(Int32 value)
    WriteLine(Int64 value)
    WriteLine(decimal value)
    WriteLine(object value)
    WriteLine(Single value)
    WriteLine(string value)
    WriteLine(UInt32 value)
    WriteLine(UInt64 value)
    WriteLine(string format, object arg1)
    WriteLine(string format, object arg1, object arg2)
    WriteLine(string format, object arg1, object arg2, object arg3)
    WriteLine(string format, params object[] args)
```

Writes text to the current test result, followed by a newline.

###Properties of the CurrentContext

####Test

Gets a representation of the current test, with the following properties:

 * **ID** - The unique Id of the test
 * **Name** - The name of the test, whether set by the user or generated automatically
 * **FullName** - The fully qualified name of the test
 * **MethodName** - The name of the method representing the test, if any
 * **Properties** - An `IPropertyBag` of the test properties

####Result

Gets a representation of the test result, with the following properties:

 * **Outcome** - A `ResultState` representing the outcome of the test. `ResultState` has the following properties:
   * **Status** - A `TestStatus` with four possible values:
     * Inconclusive
     * Skipped
     * Passed
     * Failed
   * **Label** - An optional string value, which can provide sub-categories for each Status. See below for a list of common outcomes supported internally by NUNit.
   * **Site** - A `FailureSite` value, indicating the stage of execution in which the test generated its result. Possible values are
     * Test
     * SetUp
     * TearDown
     * Parent
     * Child

Although the outcome of the test may be accessed during setup or test execution, it only has a useful value in the teardown stage.

#####Common Outcomes

The following is a list of outcomes currently produced by NUnit. Others may be added in the future.
   * Success: the test passed. (Status=Passed)
   * Inconclusive: the test was inconclusive. (Status=Inconclusive)
   * Failure: a test assertion failed. (Status=Failed, Label=empty)
   * Error = an unexpected exception occurred. (Status=Failed, Label=Error)
   * NotRunnable: the test was invalid and could not be run. (Status=Failed, Label=Invalid)
   * Cancelled: the user cancelled while this test was running. (Status=Failed, Label=Cancelled)
   * Ignored: the test was ignored. (Status=Skipped, Label=Ignored)
   * Explicit: the test was not run because it is marked Explicit. (Status=Skipped, Label=Explicit)
   * Skipped: the test was skipped for some other reason. (Status=Skipped, Label=empty)

####TestDirectory

Gets the full path of the directory containing the current test assembly. Not available in the Silverlight or Portable builds.

####WorkDirectory

Gets the full path of the directory to be used for output from this test run. The XML result file and any redirected output files are located under this directory. This is normally the directory that was current when execution of
NUnit began but may be changed by use of the **--work** option of nunit-console.

####Random

Returns a `Randomizer` object, which may be used in the test code to generate random values. These values are repeatable on reruns of the tests so long as (a) the test assembly is not changed and (b) the same seed is used. The initial random seed used in any test run may be found in the XML result file and may be provided to a subsequent run on the command line.

See [[Randomizer Methods]] for details about each available random data type.
