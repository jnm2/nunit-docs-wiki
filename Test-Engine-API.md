> **NOTE:** This page requires updates.

The NUnit Test Engine API is our first published API for discovering, exploring and executing tests programmatically. Previously, third-party runners have had to use unsupported internal classes and methods in order to execute NUnit tests.  With the development of the Engine API, this is no longer necessary.

#### Objectives of the API

The API was developed with a number of objectives in mind:

* To provide a public, published API for discovering and executing NUnit tests, suitable for use by the NUnit console and Gui runners as well as by third parties.
* To allow discovery and execution of NUnit tests independent of the particular build or version of the framework used and without the need to reference the framework itself.
* To allow future development of drivers for other frameworks and for those tests to be discovered and executed in the same way as NUnit tests.
* To provide specific features beyond the frameworks, including
  * Determining how and where each test assembly is loaded and executed.
  * Parsing project files of various types and using them to determine the location of test assemblies and the options to be used in executing them.
  * Providing access to NUnit settings for a machine.
  * Other engine-layer features may be  introduced as new versions are created.
* To isolate client runners from the engine itself, so that any updated engine installed will become immediately available to all clients on a machine without the need to upgrade the client.

#### Overview

The Engine API is included in the `nunit.engine.api` assembly, which must be referenced by any runners wanting to use it. This assembly is being released as version 3.0, to coincide with the versioning of other NUnit components. 

The actual engine is contained in the `nunit.engine` assembly. This assembly is **not** referenced by the runners. Instead, the API is used to locate and load an appropriate version of the engine, returning an instance of the `ITestEngine` interface to the  runner.

#### Getting an Instance of the Engine

The static class [TestEngineActivator](../../../nunit/blob/master/src/NUnitEngine/nunit.engine.api/TestEngineActivator.cs) is used to get an interface to the engine. It's `CreateInstance` member currently has the first overload listed. The added overloads are proposed enhancements. Additional overloads used for testing are found in the code itself.

```C#
public static ITestEngine CreateInstance(bool privateCopy = false);
public static ITestEngine CreateInstance(Version minVersion bool privateCopy = false);
```

We search for the engine in a standard set of locations, starting with the current ApplicationBase. If `privateCopy` is true, then only the ApplicationBase is examined. If no engine is found that satisfies the minimum version requirement, an exception is thrown.

We encourage authors of runners to **not** use the private copy feature, but they may use it if they do not want to rely on the user already having the engine installed. We suggest any installation of a local copy of the engine be optional in the install program.

##### Test Engine Search Order

[REWRITE] To be defined. In the current Alpha, the engine must be in the same directory as the runner exe.

#### Key Interfaces

The runner deals with the engine through a set of interfaces. These are quite general because we hope to avoid many changes to this API.

##### [ITestEngine](../../../nunit/blob/master/src/NUnitEngine/nunit.engine.api/ITestEngine.cs)

This is the primary interface to the engine. The normal sequence of calls for initially accessing it is:

```C#
ITestEngine engine = TestEngineActivator.CreateInstance(...);
engine.WorkDirectory = ...; // Defaults to the current directory
engine.InternalTraceLevel = ...; // Defaults to Off
```

The engine provides a number of services, some internal and some public. Public services are those for which the interface is publicly defined in the nunit.engine.api assembly. Internal services are... well, internal to the engine. See below for a list of public services available to runners.

The final and probably most frequently used method on the interface is `GetRunner`. It takes a `TestPackage` and returns an `ITestRunner` that is appropriate for the options specified.

##### [ITestRunner](../../../nunit/blob/master/src/NUnitEngine/nunit.engine.api/ITestRunner.cs)

This interface allows loading test assemblies, exploring the tests contained in them and running the tests. For the most common use cases, it isn't necessary to call `Load`, `Unload` or `Reload`. Calling either `Explore`, `Run` or `RunAsync` will cause the tests to be loaded automatically.

The `Explore` methods returns an `XmlNode` containing the description of all tests found. The `Run` method returns an `XmlNode` containing the results of every test. The XML format for results is the same as that for the exploration of tests, with additional nodes added to indicate the outcome of the test. `RunAsync` returns an `ITestRun` interface, which allows retrieving the XML result when it is complete.

The progress of a run is reported to the `ITestEventListener` passed to one of the run methods. Notifications received on this interface are strings in XML format, rather than XmlNodes, so that they may be passed directly across a Remoting interface.

##### Engine Services

The engine `Services` property exposes the [IServiceLocator](../../../nunit/blob/master/src/NUnitEngine/nunit.engine.api/IServiceLocator.cs) interface, which allows the runner to use public services of the engine. The following services are available publicly.

| Service            | Interface    | Function  |
|--------------------|--------------|-----------|
| ProjectService     | [IProjectLoader](../../../nunit/blob/master/src/NUnitEngine/nunit.engine.api/Extensibility/IProjectLoader.cs)  | Loads projects in various formats |
| RecentFilesService | [IRecentFiles](../../../nunit/blob/master/src/NUnitEngine/nunit.engine.api/IRecentFiles.cs)  | Provides information about recently opened files  |
| ResultService      | [IResultService](../../../nunit/blob/master/src/NUnitEngine/nunit.engine.api/IResultService.cs)  | Produces test result output in various formats  |
| SettingsService    | [ISettings](../../../nunit/blob/master/src/NUnitEngine/nunit.engine.api/ISettings.cs) | Provides access to user settings |
| LoggingService     | [ILogging](../../../nunit/blob/master/src/NUnitEngine/nunit.engine.api/ILogging.cs) | Provides centralized internal trace logging for both the engine and runners (NYI) |

The following services are used internally by the engine but are not exposed publicly but could be in the future:

| Service                  | Function  |
|--------------------------|-----------|
| TestRunnerFactory        | Creates test runners based on the TestPackage content |
| DomainManager            | Creates and manages AppDomains used to run tests      |
| DriverService            | Provides the runner with a framework driver suitable for a given assembly |
| RuntimeFrameworkSelector | Determines the runtime framework to be used in running a test |
| TestAgency               | Creates and manages Processes used to run tests       |

##### Extensibility Interfaces

The following interfaces are used by addins that extend the engine:

| Interface              | Addin Function  |
|------------------------|-----------------|
| [IProjectLoader](../../../nunit/blob/master/src/NUnitEngine/nunit.engine.api/Extensibility/IProjectLoader.cs)       | Load projects in a particular format. |
| [IProject](../../../nunit/blob/master/src/NUnitEngine/nunit.engine.api/Extensibility/IProject.cs)             | Project returned by IProjectLoader |
| [IDriverFactory](../../../nunit/blob/master/src/NUnitEngine/nunit.engine.api/Extensibility/IDriverFactory.cs)       | Provide a driver to interface with a test framework. |
| [IFrameworkDriver](../../../nunit/blob/master/src/NUnitEngine/nunit.engine.api/Extensibility/IFrameworkDriver.cs)     | Driver returned by IDriverFactory |
| [IResultWriterFactory](../../../nunit/blob/master/src/NUnitEngine/nunit.engine.api/Extensibility/IResultWriterFactory.cs) | Provide a result writer to produce an output file in a specified format |
| [IResultWriter](../../../nunit/blob/master/src/NUnitEngine/nunit.engine.api/Extensibility/IResultWriter.cs)        | Result writer returned by IResultWriterFactory |
