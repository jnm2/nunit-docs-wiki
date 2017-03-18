> **NOTE:** This page is a specification that was used as a starting point for creating the feature in NUnit. It needs to be reviewed and revised in order to accurately reflect what was actually built. If you take it with a grain of salt, it may still be helpful to you as documentation. This notice will be removed when the page is brought up to date.

The NUnit 3.0 Framework API consists of a number of related classes with well-known names contained in the framework. The 3.0 Framework Driver, which is part of the engine, performs actions by creating these classes. All required actions are performed in the constructor. The driver only needs to know the names of the classes and the arguments each one accepts.

This specification describes the interface between the 3.0 driver and framework and the rules that must be followed to provide continued backward compatibility as new versions of the framework are created.

> The API described here is specific to NUnit 3.0 and later. To run NUnit 2.x tests, a separate driver would need to be written.

The following is a simplified example of how a calling program might use the framework to load and run tests in a particular AppDomain. Note that this sort of code is expected to reside only in a driver. User-created runners should use the Engine API rather than dealing with the framework at this low level. See below for explanations of each call.

```C#
var myHandler = new MyHandlerClass(); // implements ICallbackEventHandler

// Create the controller
var args = new object[] { "my.test.assembly.dll", new Hashtable()};
var controller = domain.CreateInstanceAndUnwrap(
    "nunit.framework", "NUnit.Framework.Api.FrameworkController",
    false, 0, null, args, null, null, null);

// Load the assembly
args = new object[] { controller, myHandler };
domain.CreateInstanceAndUnwrap(
    "nunit.framework", "NUnit.Framework.Api.FrameworkController+LoadTestsAction",
    false, 0, null, args, null, null, null);

// myHandler.GetCallbackResult() should return an Xml string with the result
// of the Load, which was passed to it by the framework. 
// We're not checking this here, as we normally would do.

// Run the tests 
args = new object[] { controller, "<filter/>", myHandler };
domain.CreateInstanceAndUnwrap(
    "nunit.framework", "NUnit.Framework.Api.FrameworkController+RunTestsAction",
    false, 0, null, args, null, null, null);

// myHandler.GetCallbackResult() should return an Xml string with the results
// of running the test, which was passed to it by the framework.
```

### API Classes

The following classes provide the API:
* DriverSettings
* FrameworkController
* FrameworkControllerAction
  * LoadTestsAction
  * CountTestsAction
  * ExploreTestsAction
  * RunTestsAction

#### DriverSettings

This static class defines constants for the names of all settings recognized by the framework. We use DriverSettings rather than constants spread throughout the code in order to keep things consistent. It is intended that a copy of this class should be used by the engine as well.

Once NUnit 3.0 is released, settings in this file should not be changed, although new settings may be added. See the code itself for a list of the settings currently in use.

#### FrameworkController
    
A FrameworkController instance is created by the driver for each test assembly that must be loaded for browsing or execution. The constructor is defined as follows:

```C#
public FrameworkController(string assemblyPath, IDictionary settings)
```

where
* **assemblyPath** is the full path to the test assembly.
* **settings** is an IDictionary containing the settings to be used in loading and running this assembly. A non-generic dictionary is used to allow for implementation of the framework on platforms that don't support Generics. [However, this may be changed.]

This constructor always succeeds, provided that the arguments are of the correct types. Any operational errors will occur when specific actions like Load or Run are taken.

#### FrameworkControllerAction

As the driver needs to perform some action, it creates a temporary instance of a class derived from FrameworkControllerAction. The constructors for all actions have the following points in common:

* They take an instance of FrameworkController as their first argument. This must be the instance originally created by the driver for the particular assembly. This instance provides a common point of communication among various actions taken against the assembly.
* Another argument, the last one, is an object that implements System.Web.UI.ICallbackEventHandler. The handler receives the result of each action and - in the case of executing tests - progress notifications.
* Due to the nature of the ICallbackEventHandler interface, the results they return are always strings. The specific content of each result depends on the particular action.
* Exceptions are only thrown in the case of completely unanticipated errors, generally meaning an error in the calling program or a bug in the framework. We don't consider things like missing or bad files or exceptions thrown in user code as unanticipated.

Some actions take the string representation of a test filter as an argument. The NUnit Engine and Framework have shared knowledge of the format of a filter. For an empty filter (no filtering) use "<filter/>".

#### LoadTestsAction

LoadTestsAction must be used before any other action can be called. Its constructor is as follows:

```C#
public LoadTestsAction(FrameworkController controller, object handler);
```

where
* **controller** is the FrameworkController instance that was created for managing the test assembly.
* **handler** is an object implementing ICallbackEventHandler, to receive the result of the load. 

The result returned from handler.GetCallbackResult() is the XML representation of the loaded test assembly. No child tests are included in the XML, since this method will be called by programs with no need for such a level of detail. Programs requiring the full tree of tests, such as Gui runners, should follow up by using the ExploreTestsAction.

If the assembly can not be found or loaded, the same result is returned, but with a RunState of NotRunnable.

#### ExploreTestsAction

ExploreTestsAction is used to get the full tree of test results, as for display in a Gui. Its constructor is as follows:

```C#
public ExploreTestsAction(FrameworkController controller, string filter, object handler);
```
where
* **controller** is the FrameworkController instance that was created for managing the test assembly.
* **filter** is the string representation of a filter in XML format to be used when counting tests.
* **handler** is an object implementing ICallbackEventHandler, to receive the result of the call. 

> NOTE: The filter argument is currently ignored by this action.

The result returned from handler.GetCallbackResult() is the XML representation of the test assembly, containing all tests that passed the filter, arranged as a tree with child tests contained within their parents.

If the assembly was not be found or unable to be loaded, a non-runnable assembly with no child tests is returned.

If this action is invoked without first invoking LoadTestsAction, an InvalidOperationException is thrown.

#### CountTestsAction

CountTestsAction is used to get the number of test cases that will be executed under a specified filter, for use in a progress display. It's constructor is as follows.

```C#
public CountTestsAction(FrameworkController controller, string filter, object handler);
```

where
* **controller** is the FrameworkController instance that was created for managing the test assembly.
* **filter** is the string representation of a filter in XML format to be used when counting tests.
* **handler** is an object implementing ICallbackEventHandler, to receive the result of the call. 

The result returned from handler.GetCallbackResult() is the string representation of the integer number of test cases that match the filter.

If the assembly was not found or unable to be loaded, "0" is returned.

If this action is invoked without first invoking LoadTestsAction, an InvalidOperationException is thrown.

#### RunTestsAction

RunTestsAction is used to execute the loaded tests. It's constructor is as follows:

```C#
public RunTestsAction(FrameworkController controller, string filter, object handler) ;
```
where
* **controller** is the FrameworkController instance that was created for managing the test assembly.
* **filter** is the string representation of a filter in XML format to be used when counting tests.
* **handler** is an object implementing ICallbackEventHandler, to receive the result of the call. 

The result returned from handler.GetCallbackResult is the XML representation of the test result, including all child results.

If the assembly was not found or could not be loaded, a non-runnable result with no child tests is returned.

If this action is invoked without first invoking LoadTestsAction, an InvalidOperationException is thrown.

### Unresolved Issues

* The existing (2.6.3) Gui runner uses BeginRun, which starts tests asynchronously. Our options are:
    ** Add BeginRun to the framework API
    ** Simulate it in the engine NUnitFrameworkDriver
    ** Simulate it in the engine DirectTestRunner
* We will need to add a CancelRun action for use with Gui runners. While we only have a console runner it's not yet needed.
