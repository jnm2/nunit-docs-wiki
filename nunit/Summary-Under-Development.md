### UNDER CONSTRUCTION

NUnit 3.0 is based on NUnit version 2, but with substantial redesign and a new codebase. This page summarizes what's different between NUnit 2.6.4, the last version 2 release, and NUnit 3.0.

## General Changes

  * The previous NUnitLite framework, released as version 1.0, is now merged with the NUnit framework.

  * The license for NUnit is now MIT / X11.

## Framework

### Platforms

 * The NUnit framework is now built for a number of different platforms:
   * .NET 4.5 (also used for runtimes greater than 4.5)
   * .Net 4.0
   * .NET 2.0
   * Portable Class Library supporting 
     * .NET 4.5+
     * .NET Core (Universal Windows Apps 10+, DNX Core 5+)
     * Windows 8
     * Windows Phone 8 (Silverlight)
     * Universal (Windows Phone 8.1+, Windows 8.1+), 
     * Xamarin (MonoTouch, MonoAndroid, Xamarin iOS Universal)
   * Silverlight 5.0
   * .NET Compact Framework 3.5

 * The Silverlight and Compact Framework builds are separate downloads for those who need them.

 * Users targeting .NET 4.0 who want to write async tests will need
   to reference the Microsoft.Bcl.Async NuGet package.

### Attributes

 * The following new attributes have been added:
   * **TestFixtureSourceAttribute** is equivalent to TestCaseSource for fixtures.
   * **RetryAttribute** allows retrying of failing tests.
   * **LevelOfParallelismAttribute** and **ParallelizableAttribute** support test execution in parallel.
   * **ApartmentAttribute** is used to specify the apartment in which a test should be run.

 * The following attributes have been modified:
   * `TestCaseAttribute` and `TestCaseData` now allow modifying the test name without replacing it entirely.
   * The RangeAttribute has been extended to support more data types including uint, long and ulong
   * The named members of the TestCaseSource and ValueSource attributes must now be static.
   * RandomAttribute has been extended to add support for new data types including uint, long, ulong, short, ushort, float, byte and sbyte
   * TestCaseAttribute now allows arguments with default values to be omitted. Additionaly, it accepts IncludePlatform and ExcludePlatform properties to specify the platforms on which the test case should be run.
   * TestFixture and TestCase attributes now enforce the requirement that a reason needs to be provided when ignoring a test.
   * SetUp, TearDown, OneTimeSetUp and OneTimeTearDown methods may now be async.
   * Multiple SetUpFixtures may be specified in a single namespace.
   * ActionAttributes now allow specification of multiple targets on the attribute as designed. This didn't work in the first alpha.
   * Action Attributes have been added with the same features as in NUnit 2.6.3.

 * Parameterized test cases now support nullable arguments.
 * Tests skipped due to ExplicitAttribute are now reported as skipped.
 * Significant improvements have been made in how NUnit deduces the type arguments of 
   generic methods based on the arguments provided.
 * The ExpectedExceptionAttribute is no longer supported. Use Assert.Throws() or Assert.That(..., Throws) instead for a more precise specification of where the exception is expected to be thrown.
 * ExpectedResult is now supported on simple (non-TestCase) tests.
 * The Ignore attribute now takes a named parameter Until, which allows specifying a date after which the test is no longer ignored.
 * The following new values are now recognized by PlatformAttribute: Win7, Win8, Win8.1, Win2012Server, Win2012ServerR2, NT6.1, NT6.2, 32-bit, 64-bit
 * ValuesAttribute may be used without any values on an enum or boolean argument. All possible values are used.

### Asserts
 * Unnecessary overloads of Assert.That and Assume.That have been removed.
 * Assert.NullOrEmpty is no longer supported (Use Is.Null.Or.Empty)
 * FileAssert.Exists and FileAssert.DoesNotExist

### Constraints
 * New SupersetConstraint and Is.SupersetOf syntax complement SubsetConstraint.
 * Added Throws.ArgumentNullException
 * When checking the equality of DateTimeOffset, you can now use the 
   WithSameOffset modifier
 * A new Constraint, **DictionaryContainsKeyConstraint**, may be used to test that a specified key is present in a dictionary.
 * Does prefix operator supplies several added constraints.
 * A new FileExistsConstraint has been added.
 * You may now specify a tolerance using Within when testing equality of DateTimeOffset values.

### Other
 * TestContext.Random has also been extended to add support for new data types including 
   uint, long, ulong, short, ushort, float, byte, sbyte and decimal
 * Added GetString methods to NUnit.Framework.Internal.RandomGenerator to 
   create repeatable random strings for testing
 * Some classes intended for internal usage that were public for testing
   have now been made internal. Additional classes will be made internal
   for the final 3.0 release.
 * The class and method names of each test are included in the output xml where applicable.
 * String arguments used in test case names are now truncated to 40 rather than 20 characters.
 * String arguments over 20 characters in length are truncated when used as part of a test name.
 * The Pairwise strategy test case generation algorithm has been improved.
 * All addin support has been removed from the framework. Documentation of NUnit 3.0 extensibility features will be published in time for the beta release. In the interim, please ask for support on the nunit-discuss list.
 * Legacy suites are no longer supported
 * TestContext now has a method that allows writing to the XML output.
 * TestContext.CurrentContext.Result now provides the error message and stack trace during teardown.
 * NUnit no longer supports void async test methods. You should use a Task return Type instead.
 * Parallel test execution is supported down to the Fixture level. Use ParallelizableAttribute to indicate types that may be run in parallel.
 * Async tests are supported for .NET 4.0 if the user has installed support for them.
 * The XML output now includes a start and end time for each test.
 * TestContext is now supported and includes an additional property, **Random**, which may be used to generate repeatable random values for use in a test.
 * The external framework API is now stable; internal interfaces are separate from API
 * Tests may be run in parallel on separate threads
 * Created new API for controlling framework
 * Support for old style tests has been removed

## NUnitLite

 * The NUnitLite report output has been standardized to match that of nunit-console.
 * The NUnitLite command-line has been standardized to match that of nunit-console where they share the same options.
 * The NUnitLite runner now produces the same output display and XML results as the console runner.
 * NUnitLite tests must reference both the nunit.framework and nunitlite assemblies.
 * NUnitLite code is now merged with NUnit
 * Added NUnitLite runner to the framework code
 * The Silverlight runner now displays output in color and includes any text output created by the tests.
 * The NUnit and NUnitLite frameworks have now been merged. There is no longer any distinction
   between them in terms of features, although some features are not available on all platforms.

## Engine

 * The format of the XML result file has been finalized and documented.
 * The engine now runs multiple test assemblies in parallel by default
 * The output XML now includes more information about the test run, including the text of the command used, any engine settings and the filter used to select tests.
 * Extensions may now specify data in an identifying attribute, for use by the engine in deciding whether to load that extension.
 * We now use Cecil to examine assemblies prior to loading them.
 * Extensions are no longer based on Mono.Addins but use our own extension framework.
 * If the target framework is not specified, test assemblies that are compiled
   to target .NET 4.5 will no longer run in .NET 4.0 compatibility mode  
 * The engine API has now been finalized. It permits specifying a minimum version of the engine that a runner is able to use. The best installed version of the engine will be loaded. Third-party runners may override the selection process by including a copy of the engine in their installation directory and specifying that it must be used.
 * The V2 framework driver now uses the event listener and test listener passed to it by the runner. This corrects several outstanding issues  caused by events not being received and allows selecting V2 tests to  be run from the command-line, in the same way that V3 tests are selected.
 * The engine is now extensible using Mono.Addins. In this release, extension points are provided for FrameworkDrivers, ProjectLoaders and OutputWriters. The following addins are bundled as a part of NUnit:
   * A FrameworkDriver that allows running NUnit V2 tests under NUnit 3.0.
   * ProjectLoaders for NUnit and Visual Studio projects.
   * An OutputWriter that creates XML output in NUnit V2 format.
 * DomainUsage now defaults to Multiple if not specified by the runner
 * A driver is now included, which allows running NUnit 2.x tests under NUnit 3.0.
 * The engine can now load and run tests specified in a number of project formats:
   * NUnit (.nunit)
   * Visual Studio C# projects (.csproj)
   * Visual Studio F# projects (.vjsproj)
   * Visual Studio Visual Basic projects (.vbproj)
   * Visual Studio solutions (.sln)
   * Legacy C++ and Visual JScript projects (.csproj and .vjsproj) are also supported
   * Support for the current C++ format (.csxproj) is not yet available
 * Creation of output files like TestResult.xml in various formats is now a
   service of the engine, available to any runner.
 * The logic of runtime selection has now changed so that each assembly runs by default
   in a separate process using the runtime for which it was built.
 * On 64-bit systems, each test process is automatically created as 32-bit or 64-bit,
   depending on the platform specified for the test assembly. 

## Console Runner

   **NOTE:** The `nunit3-console` runner cannot run tests that reference the portable build. 
   You may run such tests using NUnitLite or a platform-specific runner.
 * The console runner program is now called `nunit3-console`.
 * Console runner output has been modified so that the summary comes at the end, to reduce the need for scrolling.
 * The console now displays all settings used by the engine to run tests as well as the filter used to select tests.
 * The console runner accepts a new option --maxagents. If multiple assemblies are run in separate processes, this value may be used to limit the number that are executed simultaneously in parallel.
 * The console runner no longer accepts the --include and --exclude options. Instead, the new --where option provides a more general way to express which tests will be executed, such as --where "cat==Fast && Priority==High". See the docs for details of the syntax.
 * The new --debug option causes NUnit to break in the debugger immediately before tests are run. This simplifies debugging, especially when the test is run in a separate process.
 * OneTimeSetUp and OneTimeTearDown failures are now shown on the test report. Individual test failures after OneTimeSetUp failure are no longer shown.
 * If the console is run without arguments, it will now display help
 * The console now defaults to not using shadowcopy. There is a new option **--shadowcopy** to turn it on if needed.
 * New options supported:
   * --testlist provides a list of tests to run in a file
   * --stoponerror indicates that the run should terminate when any test fails.
 * The command-line may now include any number of assemblies and/or supported projects.
 * The console runner now runs tests in a separate process per assembly by default. They may
   still be run in process or in a single separate process by use of command-line options.
 * The console runner now starts in the highest version of the .NET runtime available, making
   it simpler to debug tests by specifying that they should run in-process on the command-line.
 * The -x86 command-line option is provided to force execution in a 32-bit process on a 64-bit system.
 * A writeability check is performed for each output result file before trying to run the tests.
 * The -teamcity option is now supported.
 * The console runner no longer displays test results in the debugger.
 * The console runner now automatically detects 32- versus 64-bit test assemblies.
 * Both nunit-console and NUnitLite now display output in color.
 * The console runner refuses to run tests build with older versions of NUnit. A plugin will be available to run older tests in the future.

## Issues Resolved

#### Github Issues

 * 6	Log4net not working with NUnit
 * 8  [SetUpFixture] is not working as expected
 * 12 Compact framework should support generic methods
 * 14 CI Server for NUnit Framework
 * 13	Standardize commandline options for nunitlite runner
 * 17	No allowance is currently made for nullable arguents in TestCase parameter conversions
 * 20 TestCaseAttribute needs Platform property.
 * 21 Is.InRange Constraint Ambiguity
 * 22 Add OSArchitecture Attribute to Environment node in result xml
 * 24 Assert on Dictionary Content
 * 27 Values attribute support for enum types
 * 29 Specifying a tolerance with "Within" doesn't work for DateTimeOffset data types
 * 31 Report start and end time of test execution
 * 33	TestCaseSource cannot refer to a parameterized test fixture
 * 36 Make RequiresThread, RequiresSTA, RequiresMTA inheritable
 * 37	Multiple SetUpFixtures should be permitted on same namespace
 * 41	Check for zeroes in Assert messages
 * 45 Need of Enddate together with Ignore
 * 47 Extensions to RangeAttribute
 * 48 Explicit seems to conflict with Ignore
 * 54	Store message and stack trace in TestContext for use in TearDown
 * 55 Incorrect XML comments for CollectionAssert.IsSubsetOf
 *  59 Length of generated test names should be limited
 * 60 NUnit should support async setup, teardown, fixture setup and fixture teardown.
 * 62   Matches(Constraint) does not work as expected
 * 63   Async support should handle Task return type without state machine
 * 64   AsyncStateMachineAttribute should only be checked by name
 * 65   Update NUnit Wiki to show the new location of samples
 * 66   Parallel Test Execution within test assemblies
 * 67   Allow Expected Result on simple tests
 *  68 Customization of test case name generation
 * 70   EquivalentTo isn't compatible with IgnoreCase for dictioneries
 * 75   Async tests should be supported for projects that target .NET 4.0
 * 82   nunit-framework tests are timing out on Linux
 * 83   Path-related tests fail on Linux
 * 85   Culture-dependent NUnit tests fail on non-English machine
 * 88   TestCaseSourceAttribute documentation
 * 90   EquivalentTo isn't compatible with IgnoreCase for char
 * 100  Changes to Tolerance definitions
 * 110  Add new platforms to PlatformAttribute
 * 111	Implement Changes to File, Directory and Path Assertions
 * 112	Implement Action Attributes
 * 113  Remove ExpectedException
 * 118  Workarounds for missing InternalPreserveStackTrace in mono
 * 121  Test harness does not honor the --worker option when set to zero
 * 125  3rd-party dependencies should be downloaded on demand
 * 129  Standardize Timeout in the Silverlight build
 * 130  Add FileAssert.Exists and FileAssert.DoesNotExist
 * 132  Drop support for void async methods
 * 145  NUnit-console fails if test result message contains invalid xml characters
 * 153  Surprising behavior of DelayedConstraint pollingInterval
 * 155  Create utility classes for platform-specific code
 * 156	Accessing multiple AppDomains within unit tests result in SerializationException
 * 161  Update API to support stopping an ongoing test run
 * 163	Add --trace option to NUnitLite
 * 167	Create interim documentation for the alpha release
 * 168  Create NUnit 3.0 documentation
 * 169	Design and implement distribution of NUnit packages
 * 171	Assert.That should work with any lambda returning bool
 * 175	Test Harness should return an error if any tests fail
 * 180	 Errors in Linux CI build
 * 181	Replace NAnt with MsBuild / XBuild
 * 183	Standardize commandline options for test harness
 * 188	No output from NUnitLite when selected test is not found
 * 189	Add string operators to Does prefix
 * 193	TestWorkerTests.BusyExecutedIdleEventsCalledInSequence fails occasionally
 * 196  Compare DateTimeOffsets including the offset in the comparison 
 * 197	Deprecate or remove Assert.NullOrEmpty
 * 202	Eliminate legacy suites
 * 203	Combine framework, engine and console runner in a single solution and repository
 * 209	Make Ignore attribute's reason mandatory
 * 210	TestContext.WriteLine in an AppDomain causes an error
 * 215	Running 32-bit tests on a 64-bit OS
 * 217  New icon for the 3.0 release
 * 219	Teardown failures are not reported
 * 222	Color console for NUnitLite
 * 223  Common code for NUnitLite console runner and NUnit-Console
 * 224	Silverlight Support
 * 225  Compact Framework Support
 * 227	Add support for VS projects and solutions
 * 229	Timing failures in tests
 * 231	Update C# samples to use NUnit 3.0
 * 233	Update F# samples to use NUnit 3.0
 * 234	Update C++ samples to use NUnit 3.0
 * 237 System.Uri .ctor works not properly under Nunit
 * 238  Improvements to running 32 bit tests on a 64 bit system
 * 241	Remove reference to Microslft BCL packages
 * 243	Create solution for Linux
 * 244 NUnit should properly distinguish between .NET 4.0 and 4.5
 * 245	Multiple targets on action attributes not implemented
 * 246	C++ tests do not compile in VS2013
 * 247	Eliminate trace display when running tests in debug
 * 254	 Finalize XML format for test results
 * 255	Add new result states for more precision in where failures occur
 * 256	ContainsConstraint break when used with AndConstraint
 * 257  TestCaseAttribute should not require parameters with default values to be specified.
 * 261  Add portable nunitlite build
 * 264	Stacktrace displays too many entries
 * 265	Reorganize console reports for nunit-console and nunitlite
 * 266  Pluggable framework drivers.
 * 269	Add manifest to nunit-console and nunit-agent
 * 270	OneTimeSetUp failure results in too much output
 * 271	Invalid tests should be treated as errors
 * 274	Command line options should be case insensitive
 * 275	NUnitEqualityComparer fails to compare IEquatable<T> where second object is derived from T
 * 276	NUnit-console should not reference nunit.framework
 * 278	New result states (ChildFailure and SetupFailure) break NUnit2XmlOutputWriter
 * 282	Get tests for NUnit2XmlOutputWriter working
 * 283 What should we do when a user extension does something bad?
 * 284  NUnitLite Unification
 * 288	Set up Appveyor CI build
 * 290	Stack trace still displays too many items
 * 293  CF does not have a CurrentDirectory
 * 299	No full path to assembly in XML file under Compact Framework
 * 301	Command-line length
 * 304	Run test Assemblies in parallel
 * 306  Assure NUnit can write resultfile
 * 308  Early disposal of runners
 * 309  NUnit-Console should support incremental output under TeamCity
 * 310 Target framework not specified on the AppDomain when running against .Net 4.5
 * 315	NUnit 3.0 alpha: Cannot run in console on my assembly
 * 316  NUnitLite TextUI Runner
 * 318	TestActionAttribute: Retrieving the TestFixture
 * 319	CI builds are not treating test failures as failures of the build
 * 320  No Tests found: Using parametrized Fixture and TestCaseSource
 * 321 Rationalize how we count tests
 * 322	Remove Stopwatch tests where they test the real .NET Stopwatch
 * 325  Add RegexConstraint to compact framework build
 * 326  Add TimeoutAttribute to compact framework build
 * 327  Allow generic test methods in the compact framework
 * 328  Use .NET Stopwatch class for compact framework builds
 * 331  Alpha 2 CF does not build
 * 333  Add parallel execution to desktop builds of NUnitLite
 * 334  Include File-related constraints and syntax in NUnitLite builds
 * 335  Re-introduce 'Classic' NUnit syntax in NUnitLite
 * 336  Document use of separate obj directories per build in our projects
 * 337  Update Standard Defines page for .NET 3.0
 * 341  Move the NUnitLite runners to separate assemblies
 * 360  Better exception message when using non-BCL class in property
 * 363	Make Xml result output an engine service
 * 367  Refactor XML Escaping Tests
 * 368  Create addin model.
 * 369  Project loader addins
 * 370  OutputWriter addins
 * 372  CF Build TestAsesemblyRunnerTests
 * 373  Minor CF Test Fixes
 * 374	New syntax for selecting tests to be run
 * 377	CombiningStrategyAttributes don't work correctly on generic methods
 * 378  Correct documentation for PairwiseAttribute
 * 386  Console Output Improvements
 * 388	Improvements to NUnitLite runner output
 * 390	Specify exactly what happens when a test times out
 * 396	ApartmentAttribute
 * 397	CF nunitlite runner assembly has the wrong name
 * 403  Move ConsoleOptions.cs and Options.cs to Common and share...
 * 404 Split tests between nunitlite.runner and nunit.framework
 * 407	Assert.Pass() with ]]> in message crashes console runner
 * 414	 Simplify Assert overloads
 * 416	NUnit 2.x Framework Driver
 * 417	 Complete work on NUnit projects
 * 419  Create Windows Installer for NUnit.
 * 420	 Create Settings file in proper location
 * 427  [TestFixture(Ignore=true)] should not be allowed.
 * 428	 Add ExpectedExceptionAttribute to C# samples
 * 437  Errors in tests under Linux due to hard-coded paths.
 * 440	 Automatic selection of Test Engine to use
 * 441  NUnit-Console should support --testlist option
 * 442  Add --stoponerror option back to nunit-console.
 * 450	 Create master install that includes the framework, engine and console installs
 * 454  Rare registry configurations may cause NUnit to fail
 * 456  Fix memory leak in RuntimeFramework.
 * 459  Remove the Mixed Platforms build configuration.
 * 468  Change default domain usage to multiple.
 * 469  Truncate string arguments in test names in order to limit the length.
 * 472 Overflow exception and DivideByZero exception from the RangeAttribute
 * 477	 Assert does not work with ArraySegment
 * 478  RepeatAttribute
 * 481  Testing multiple assemblies in nunitlite
 * 482 	nunit-console has multiple errors related to -framework option
 * 483	Adds constraint for asserting that a dictionary contains a particular key
 * 484	Missing file in NUnit.Console nuget package
 * 485	Can't run v2 tests with nunit-console 3.0
 * 487	NUnitLite can't load assemblies by their file name
 * 488	Async setup and teardown still don't work
 * 497	Framework installer shold register the portable framework
 * 504	Option --workers:0 is ignored
 * 508	Travis builds with failure in engine tests show as successful
 * 509	Under linux, not all mono profiles are listed as available
 * 512	Drop the .NET 3.5 build
 * 515	OSPlatform.IsMacOSX doesn't work
 * 517	V2 FrameworkDriver does not make use of passed in TestEventListener
 * 523	 Provide an option to disable shadowcopy in NUnit v3
 * 524 int and char do not compare correctly?
 * 528	V2 FrameworkDriver does not make use of passed in TestFilter
 * 530	Color display for Silverlight runner
 * 531	Display text output from tests in Silverlight runner
 * 534	Add classname and methodname to test result xml
 * 538  Potential bug using TestContext in constructors
 * 539 Truncation of string arguments
 * 541	Console help doesn't indicate defaults
 * 544 AsyncTestMethodTests for 4.5 Framework fails frequently on Travis CI
 * 546  Enable Parallel in NUnitLite/CF (or more) builds
 * 551  TextRunner not passing the NumWorkers option to the ITestAssemblyRunner
 * 556  Executed tests should always return a non-zero duration
 * 559  Fix text of NuGet packages
 * 560  Fix PackageVersion property on wix install projects
 * 562  Program.cs in NUnitLite NuGet package is incorrect
 * 564  NUnitLite Nuget package is Beta 1a, Framework is Beta 1
 * 565  NUnitLite Nuget package adds Program.cs to a VB Project
 * 568  Isolate packaging from building
 * 570  ThrowsConstraint failure message should include stack trace of actual exception
 * 573	nunit-console hangs on Mac OS X after all tests have run
 * 575 Add support for ASP.NET 5 and the new Core CLR
 * 576  Throws.ArgumentNullException would be nice
 * 577  Documentation on some members of Throws falsely claims that they return `TargetInvocationException` constraints
 * 579  No documentation for recommended usage of TestCaseSourceAttribute
 * 580  TeamCity Service Message Uses Incorrect Test Name with NUnit2Driver
 * 582  Test Ids Are Not Unique
 * 583  TeamCity service messages to support parallel test execution
 * 584  Non-runnable assembly has incorrect ResultState
 * 585 RetryAttribute
 * 609  Add support for integration with TeamCity
 * 611  Remove unused --teamcity option from CF build of NUnitLite
 * 612  MaxTime doesn't work when used for TestCase
 * 621  Core Engine
 * 622  nunit-console fails when use --output
 * 628  Modify IService interface and simplify ServiceContext
 * 631  Separate packaging for the compact framework
 * 642 Restructure MSBuild script
 * 646  ConfigurationManager.AppSettings Params Return Null under Beta 1
 * 649 Change how we zip packages
 * 654 ReflectionOnlyLoad and ReflectionOnlyLoadFrom
 * 656 Unused parameter in Console.WriteLine found
 * 664 Invalid "id" attribute in the report for case "test started"
 * 669	TeamCity service message should have assembly name as a part of test name.
 * 670 Failing Tests in TeamCity Build
 * 673 Ensure proper disposal of engine objects
 * 674 Engine does not release test assemblies
 * 679 Windows 10 Support
 * 682 Add Async Support to Portable Framework
 * 683 Make FrameworkController available in portable build
 * 685 In the some cases when tests cannot be started NUnit returns exit code "0"
 * 687 TestAgency does not launch agent process correctly if runtime type is not specified (i.e. v4.0)
 * 689	The TeamCity service message "testFinished" should have an integer value in the "duration" attribute
 * 692 PlatformAttribute_OperatingSystemBitNess fails when running in 32-bit process
 * 693 Generic Test<T> Method cannot determine type arguments for fixture when passed as IEnumerable<T>
 * 698 Require TestCaseSource and ValueSource named members to be static
 * 703 TeamCity non-equal flowid for 'testStarted' and 'testFinished' messages
 * 712 Extensions to RandomAttribute
 * 713	Include command information in XML
 * 715 Provide a data source attribute at TestFixture Level
 * 718 RangeConstraint gives error with from and two args of differing types
 * 719	We have no way to configure tests for several assemblies using NUnit project file and the common installation from msi file
 * 723 Does nunit.nuspec require dependency on Microsoft.Bcl.Async? 
 * 724 Adds support for Nullable<bool> to Assert.IsTrue and Assert.IsFalse
 * 728 Missing Assert.That overload
 * 734 Console without parameters doesn't show help
 * 735	Workers number in xml report file cannot be found
 * 741 Explicit Tests get run when using --exclude
 * 746 Framework should send events for all tests
 * 747 NUnit should apply attributes even if test is non-runnable
 * 749 Review Use of Mono.Addins for Engine Extensibility
 * 750 Include Explicit Tests in Test Results
 * 753 Feature request: Is.SupersetOf() assertion constraint
 * 755 TimeOut attribute doesn't work with TestCaseSource Attribute
 * 757 Implement some way to wait for execution to complete in ITestEngineRunner
 * 760 Packaging targets do not run on Linux
 * 766 Added overloads for True()/False() accepting booleans
 * 778 Build and build.cmd scripts invoke nuget.exe improperly
 * 780 Teamcity fix
 * 782 No sources for 2.6.4
 * 783 Package separately for Silverlight
 * 784	Build Portable Framework on Linux
 * 790	Allow Extensions to provide data through an attribute
 * 794	Make it easier to debug tests as well as NUnit itself
 * 801	NUnit calls Dispose multiple times
 * 814	Support nullable types with TestCase
 * 818	Possible error in Merge Pull Request #797
 * 821	Wrapped method results in loss of result information
 * 822	Test for Debugger in NUnitTestAssemblyRunner probably should not be in CF build
 * 824	Remove unused System.Reflection using statements
 * 826	Randomizer uniqueness tests fail randomly!
 * 828 	Merge pull request #827 (issue 826)
 * 830	Add ability to report test results synchronously to test runners
 * 833 Intermittent failure of WorkItemQueueTests.StopQueue_WithWorkers
 * 837	Enumerators not disposed when comparing IEnumerables
 * 840	Add missing copyright notices
 * 844	Pull Request #835 (Issue #814) does not build in CF
 * 847	 Add new --process:inprocess and --inprocess options
 * 850	Test runner fails if test name contains invalid xml characters
 * 851	 'Exclude' console option is not working in NUnit Lite
 * 853	Cannot run NUnit Console from another directory
 * 859 NUnit-Console output - move Test Run Summary to end
 * 860	Use CDATA section for message, stack-trace and output elements of XML
 * 863	Eliminate core engine
 * 865	Intermittent failures of StopWatchTests
 * 867 Remove Warnings from Ignored tests
 * 868 Review skipped tests
 * 869	Tests that use directory separator char to determine platform misreport Linux on MaxOSX
 * 870	NUnit Console Runtime Environment misreports on MacOSX
 * 874 	Add .NET Core Framework
 * 878	Cannot exclude MacOSX or XBox platforms when running on CF
 * 887 Move environment and settings elements to the assembly suite in the result file
 * 892	Fixed test runner returning early when executing more than one test run.
 * 894	Give nunit.engine and nunit.engine.api assemblies strong names
 * 896	NUnit 3.0 console runner not placing test result xml in --work directory
 * 899 Colors for ColorConsole on grey background are too light
 * 904 InternalPreserveStackTrace is not supported on all Portable platforms
 * 914 Unclear error message from console runner when assembly has no tests
 * 916 Console runner dies when test agent dies
 * 918 Console runner --where parameter is case sensitive
 * 920 Remove addins\nunit.engine.api.dll from NuGet package
 * 929 Rename nunit-console.exe
 * 931 Remove beta warnings from NuGet packages
 * 936 Explicit skipped tests not displayed
 * 939 Installer complains about .NET even if already installed
 * 940 Confirm or modify list of packages for release
 * 947 Breaking API change in ValueSourceAttribute
 * 949 Update copyright in NUnit Console
 * 954 NUnitLite XML output is not consistent with the engine's
 * 955 NUnitLite does not display the where clause
 * 959 Restore filter options for NUnitLite portable build
 * 960 Intermittent failure of CategoryFilterTests
 * 967 Run Settings Report is not being displayed.

#### GitHub Issues from former nunit-console repository

 * 2	Failure in TestFixtureSetUp is not reported correctly
 * 5	CI Server for nunit-console
 * 6	System.NullReferenceException on start nunit-console-x86
 * 21	NUnitFrameworkDriverTests fail if not run from same directory
 * 24	'Debug' value for /trace option is deprecated in 2.6.3
 * 38	Confusing Excluded categories output

#### Launchpad Bugs

   * 400502 	NUnitEqualityComparer.StreamsE­qual fails for same stream
   * 400508 	TestCaseSource attirbute is not working when Type is given
   * 400510 	TestCaseData variable length ctor drops values
   * 417557 	Add SetUICultureAttribute from NUnit 2.5.2
   * 417559 	Add Ignore to TestFixture, TestCase and TestCaseData
   * 417560 	Merge Assert.Throws and Assert.Catch changes from NUnit 2.5.2
   * 417564 	TimeoutAttribute on Assembly
   * 419411 	Fixture With No Tests Shows as Non-Runnable
   * 430100 	Assert.Catch<T> should return T
   * 432566 	NUnitLite shows empty string as argument
   * 432573 	Mono test should be at runtime
   * 432805 	Some Framework Tests don't run on Linux
   * 440109 	Full Framework does not support "Contains"
   * 459219 	Changes to thread princpal cause failures under .NET 4.0
   * 459224 	Culture test failure under .NET 4.0
   * 462019 	Line endings needs to be better controlled in source
   * 462418 	Assume.That() fails if I specify a message
   * 463470 	We should encapsulate references to pre-2.0 collections
   * 483836 	Allow non-public test fixtures consistently
   * 483845 	TestCase expected return value cannot be null
   * 487878 	Tests in generic class without proper TestFixture attribute should be invalid
   * 488002 	Should not report tests in abstract class as invalid
   * 490679 	Category in TestCaseData clashes with Category on ParameterizedMethodSuite
   * 498656 	TestCase should show array values in GUI
   * 498690 	Assert.That() doesn't like properties with scoped setters
   * 501352 	VS2010 projects have not been updated for new directory structure
   * 501784 	Theory tests do not work correctly when using null parameters
   * 504018 	Automatic Values For Theory Test Parameters Not Provided For bool And enum
   * 505899 	'Description' parameter in both TestAttribute and TestCaseAttribute is not allowed
   * 513989 	Is.Empty should work for directories
   * 519912 	Thread.CurrentPrincipal Set In TestFixtureSetUp Not Maintained Between Tests
   * 523335 	TestFixtureTearDown in static class not executed
   * 531873 	Feature: Extraction of unit tests from NUnit test assembly and calling appropriate one
   * 532488 	constraints from ConstraintExpression/ConstraintBuilder are not reusable
   * 556971 	Datapoint(s)Attribute should work on IEnumerable<T> as well as on Arrays
   * 561436 	SetCulture broken with 2.5.4
   * 563532 	DatapointsAttribute should be allowed on properties and methods
   * 590717 	categorie contains dash or trail spaces is not selectable
   * 590970 	static TestFixtureSetUp/TestFixtureTearDown methods in base classes are not run
   * 595683 	NUnit console runner fails to load assemblies
   * 600627 	Assertion message formatted poorly by PropertyConstraint
   * 601108 	Duplicate test using abstract test fixtures
   * 601645 	Parametered test should try to convert data type from source to parameter
   * 605432 	ToString not working properly for some properties
   * 606548 	Deprecate Directory Assert in 2.5 and remove it in 3.0
   * 608875 	NUnit Equality Comparer incorrectly defines equality for Dictionary objects
   * 611325 	Allow Teardown to detect if last test failed
   * 611938 	Generic Test Instances disappear
   * 655882 	Make CategoryAttribute inherited
   * 664081 	Add Server2008 R2 and Windows 7 to PlatformAttribute
   * 671432 	Upgrade NAnt to Latest Release
   * 676560 	Assert.AreEqual does not support IEquatable<T>
   * 691129 	Add Category parameter to TestFixture
   * 697069 	Feature request: dynamic location for TestResult.xml
   * 708173 	NUnit's logic for comparing arrays - use Comparer<T[]> if it is provided
   * 709062 	"System.ArgumentException : Cannot compare" when the element is a list
   * 712156 	Tests cannot use AppDomain.SetPrincipalPolicy
   * 719184 	Platformdependency in src/ClientUtilities/util/Services/DomainManager.cs:40
   * 719187 	Using Path.GetTempPath() causes conflicts in shared temporary folders
   * 735851 	Add detection of 3.0, 3.5 and 4.0 frameworks to PlatformAttribute
   * 736062 	Deadlock when EventListener performs a Trace call + EventPump synchronisation
   * 756843 	Failing assertion does not show non-linear tolerance mode
   * 766749 	net-2.0\nunit-console-x86.exe.config should have a <startup /> element and also enable loadFromRemoteSources
   * 770471 	Assert.IsEmpty does not support IEnumerable
   * 785460 	Add Category parameter to TestCaseSourceAttribute
   * 787106 	EqualConstraint provides inadequate failure information for IEnumerables
   * 792466 	TestContext MethodName
   * 794115 	HashSet incorrectly reported
   * 800089 	Assert.Throws() hides details of inner AssertionException
   * 848713 	Feature request: Add switch for console to break on any test case error
   * 878376 	Add 'Exactly(n)' to the NUnit constraint syntax
   * 882137 	When no tests are run, higher level suites display as Inconclusive
   * 882517 	NUnit 2.5.10 doesn't recognize TestFixture if there are only TestCaseSource inside
   * 885173 	Tests are still executed after cancellation by user
   * 885277 	Exception when project calls for a runtime using only 2 digits
   * 885604 	Feature request: Explicit named parameter to TestCaseAttribute
   * 890129 	DelayedConstraint doesn't appear to poll properties of objects
   * 892844 	Not using Mono 4.0 profile under Windows
   * 893919 	DelayedConstraint fails polling properties on references which are initially null
   * 896973 	Console output lines are run together under Linux
   * 897289 	Is.Empty constraint has unclear failure message
   * 898192 	Feature Request: Is.Negative, Is.Positive
   * 898256 	IEnumerable<T> for Datapoints doesn't work
   * 899178 	Wrong failure message for parameterized tests that expect exceptions
   * 904841 	After exiting for timeout the teardown method is not executed
   * 908829 	TestCase attribute does not play well with variadic test functions
   * 910218 	NUnit should add a trailing separator to the ApplicationBase
   * 920472 	CollectionAssert.IsNotEmpty must dispose Enumerator
   * 922455 	Add Support for Windows 8 and Windows 2012 Server to PlatformAttribute
   * 928246 	Use assembly.Location instead of assembly.CodeBase
   * 958766 	For development work under TeamCity, we need to support nunit2 formatted output under direct-runner
   * 1000181 	Parameterized TestFixture with System.Type as constructor arguments fails
   * 1000213 	Inconclusive message Not in report output
   * 1023084 	Add Enum support to RandomAttribute
   * 1028188 	Add Support for Silverlight
   * 1029785 	Test loaded from remote folder failed to run with exception System.IODirectory
   * 1037144 	Add MonoTouch support to PlatformAttribute
   * 1041365 	Add MaxOsX and Xbox support to platform attribute
   * 1057981 	C#5 async tests are not supported
   * 1060631 	Add .NET 4.5 build
   * 1064014 	Simple async tests should not return Task<T>
   * 1071164 	Support async methods in usage scenarios of Throws constraints
   * 1071343 	Runner.Load fails on CF if the test assembly contains a generic method
   * 1071861 	Error in Path Constraints
   * 1072379 	Report test execution time at a higher resolution
   * 1074568 	Assert/Assume should support an async method for the ActualValueDelegate
   * 1082330 	Better Exception if SetCulture attribute is applied multiple times
   * 1111834 	Expose Random Object as part of the test context
   * 1111838 	Include Random Seed in Test Report
   * 1172979 	Add Category Support to nunitlite Runner
   * 1203361 	Randomizer uniqueness tests sometimes fail
   * 1221712 	When non-existing test method is specified in -test, result is still "Tests run: 1, Passed: 1"
   * 1223294 	System.NullReferenceException thrown when ExpectedExceptionAttribute is used in a static class
   * 1225542 	Standardize commandline options for test harness

	
### Earlier Releases


 * Release Notes for <a href="http://www.nunit.org/?p=releaseNotes&r=2.6.4">NUnit 2.6 through 2.6.4</a>
 * Release Notes for <a href="http://www.nunit.org/?p=releaseNotes&r=2.5.10">NUnit 2.5 through 2.5.10</a>
 * Release Notes for <a href="http://www.nunit.org/?p=releaseNotes&r=2.4.8">NUnit 2.4 through 2.4.8</a>
 * Release Notes for <a href="http://www.nunit.org/?p=releaseNotes&r=2.2.10">NUnit 2.0 through 2.2.10</a>

