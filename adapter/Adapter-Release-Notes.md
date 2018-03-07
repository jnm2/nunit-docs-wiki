#### NUnit3 Test Adapter for Visual Studio - Version 3.10 - March 5, 2018

#####  Features

* [461](https://github.com/nunit/nunit3-vs-adapter/issues/461)  Publish symbols with the adapter for debugging into the adapter and nunit, see 

##### Resolved Issues
* [47](https://github.com/nunit/nunit3-vs-adapter/issues/47)  Adapter runs explicit tests when TFS TestCaseFilter is used
* [296](https://github.com/nunit/nunit3-vs-adapter/issues/296) Mono.Cecil causes OutOfMemoryException with new .csproj PDBs  
* [310](https://github.com/nunit/nunit3-vs-adapter/issues/310) Consistent Category Display in Test Explorer Window 
* [365](https://github.com/nunit/nunit3-vs-adapter/issues/365) An exception occurred while invoking executor: Could not load file or assembly System.Runtime.InteropServices.RuntimeInformation (Thanks to [halex2005](https://github.com/halex2005) for [PR 418](https://github.com/nunit/nunit3-vs-adapter/pull/418))
* [419](https://github.com/nunit/nunit3-vs-adapter/issues/419)  Test result is Skipped when an exception has been thrown and the only warning is in TearDown
* [444](https://github.com/nunit/nunit3-vs-adapter/issues/444)  Dump file is not created when the test crashes
* [452](https://github.com/nunit/nunit3-vs-adapter/issues/452) Adapter does not seem to respect any TestCategory filtering 
* [460](https://github.com/nunit/nunit3-vs-adapter/issues/460)  Failure to load dependency assembly causes hang

Also see [Release Readiness Review](https://github.com/nunit/nunit3-vs-adapter/issues/472)  

#####  Special thanks
Special thanks to :  [Joseph Musser](https://github.com/jnm2) for awesome work on this release,

and to [Loren Halvorsen](https://www.linkedin.com/in/lorenhalvorson/) for the workaround for VSTest [issue 261](https://github.com/nunit/nunit3-vs-adapter/issues/261#issuecomment-259970442).  


#### NUnit3 Test Adapter for Visual Studio - Version 3.9 - October 29, 2017

##### Change in supported versions

This version supports Visual Studio from version 2012, Update 1 and upwards, and all subsequent versions in 2013, 2015 and 2017.  Visual Studio 2012 RTM is then no longer supported.


##### Features


* [390](https://github.com/nunit/nunit3-vs-adapter/issues/390) Pass DisableAppDomain and DisableParallelization settings to the Engine
* [392](https://github.com/nunit/nunit3-vs-adapter/issues/392) Improve performance of discovery (Thanks to [Navin (Microsoft)](https://github.com/navin22) for [PR 393](https://github.com/nunit/nunit3-vs-adapter/pull/393), [PR 406](https://github.com/nunit/nunit3-vs-adapter/pull/406) )
* [394](https://github.com/nunit/nunit3-vs-adapter/issues/394) The adapter tests are updated to use NUnit 3.8.1



##### Resolved Issues


* [372](https://github.com/nunit/nunit3-vs-adapter/issues/372) netcoreapp + CultureInfo.CurrentCulture = bad time  (Thanks to [Aaron Housh (Dispersia)](https://github.com/Dispersia)  for [PR 380](https://github.com/nunit/nunit3-vs-adapter/pull/380) )
* [386](https://github.com/nunit/nunit3-vs-adapter/issues/386) DateTime.Parse issue during test discovery with certain cultures  (Also fixed by  [PR 380](https://github.com/nunit/nunit3-vs-adapter/pull/380) )
* [302](https://github.com/nunit/nunit3-vs-adapter/issues/302) BadImageFormatException building solution with unmanaged projects



#### NUnit3 Test Adapter for Visual Studio - Version 3.8 - July 19, 2017

##### Features

 * The adapter now support running .net core projects. See [this post](http://www.alteridem.net/2017/05/04/test-net-core-nunit-vs2017/) for details.  Note: Only supported by the nuget adapter, not the vsix. 
 * The adapter now uses version 3.7 of the engine to run tests ([360](https://github.com/nunit/nunit3-vs-adapter/issues/360))
 * Attachments can be added to tests ([358](https://github.com/nunit/nunit3-vs-adapter/issues/358))
 * Prepared for new  upcoming Test Explorer functionality, as documented in this [RFC](https://github.com/Microsoft/vstest-docs/blob/master/RFCs/0010-Source-Information-For-Discovered-Tests.md)  ([351](https://github.com/nunit/nunit3-vs-adapter/issues/351))


##### Resolved Issues

* [298](https://github.com/nunit/nunit3-vs-adapter/issues/298) $RANDOM_SEED$ is appearing in non-test project build output
* [259](https://github.com/nunit/nunit3-vs-adapter/issues/259) An exception occurred while invoking executor 'executor://nunit3testexecutor/'
* [314](https://github.com/nunit/nunit3-vs-adapter/issues/314) Any TestFixture deriving from a base-class which defines unit-tests will fail when the base-class is from another class-library
* [231](https://github.com/nunit/nunit3-vs-adapter/issues/231) Improved message on failed loading. See also [PR 309](https://github.com/nunit/nunit3-vs-adapter/pull/309)
* [338](https://github.com/nunit/nunit3-vs-adapter/issues/338) Unhandled Exception when running through vstest.console.exe /listtests



#### NUnit3 Test Adapter for Visual Studio - Version 3.7 - January 25, 2017

##### Features

 * The adapter now uses version 3.6 of the engine to run tests
 * Warning messages are displayed. Note that Visual Studio currently lists them as skipped.
 * Multiple assertion failures in a Multiple Assert block are displayed.

##### Resolved Issues

 * 218 No tests found to run when TestFixture is a nested class
 * 256 Rename $RANDOM_SEED$
 * 258 Modify adapter to display multiple assert information
 * 268 Make the Icon Larger
 * 272 URL for "More information" should point to correct landing page
 * 273 Report Warnings in VS adapter
 * 276 Adapter requires test project pbd's to be generated for tests to be executed
 * 288 Test parameters containing semicolons are truncated

#### NUnit3 Test Adapter for Visual Studio - Version 3.6.1 - December 5, 2016

> **Note:** This was a hotfix release of the vsix package only, fixing an issue that prevented it from installing under VS2012 and 2013.

##### Resolved Issues

 * 260 VSIX no longer visible in Visual Studio 2012

#### NUnit3 Test Adapter for Visual Studio - Version 3.6 - November 15, 2016

##### Features

 * Adds support for Visual Studio "15"

##### Resolved Issues

 * 253 Warnings about $RANDOM_SEED$ during build
 * 262 Support for VS 15

#### NUnit3 Test Adapter for Visual Studio - Version 3.5 - October 22, 2016

##### Features

 * The adapter now uses version 3.5 of the NUnit engine
 * The NuGet package is now installed as a tool and no longer creates unnecessary references in the project

##### Resolved Issues

 * 97 Tests with dynamic/random parameters are never run closed:done is:bug pri:normal
 * 204 If a test writes to Console.Error, the test passes but the session fails
 * 220 Visual Studio Test Adapter - Writing to test output throws an error
 * 221 Change adapter package to use tools directory
 * 236 Update adapter to use Version 3.5 of the Engine
 * 238 Just warn upon failing to restore random seed
 * 239 Remove Error-level log messages from adapter where we don't want run to fail
 * 243 NuGet package and copy local

#### NUnit3 Test Adapter for Visual Studio - Version 3.4.1 - August 5, 2016

##### Features

 * We now use Cake to build and package the adapter.

##### Resolved Issues

 * 198 Create Cake script for build
 * 202 NUnit3 Test Adapter not running all tests in Visual Studio 2015
 * 205 Adapter fails to find Mono.Cecil when targeting .NET 3.5

#### NUnit3 Test Adapter for Visual Studio - Version 3.4 - July 2, 2016

##### Features

 * The adapter now uses the NUnit 3.4.1 TestEngine.
 * TestRunParameters may now be provided in the `.runsettings` file.
 * Immediate text output from tests now displays in the Output window. This includes any output produced through Console.Error, TestContext.Error or TestContext.Progress.

##### Resolved Issues

 * 132 Print to console not shown with v3 of adapter
 * 138 Cannot run navigation tests under the console runner
 * 145 Implement TestRunParameters inside .runsettings for runtime parameters
 * 180 Upgrade to NUnit 3.4.1
 * 181 Can't run requiring a 32-bit process
 * 183 Use Mono.Cecil to retrieve source code locations
 * 190 NUnit30Settings.xml is used by other process leads to hidden tests
 * 192 Corrupt NUnit3Settings.xml causes crash

#### NUnit3 Test Adapter for Visual Studio - Version 3.2 - June 3, 2016

##### Features

 * The adapter now uses the NUnit 3.2.1 TestEngine.

##### Resolved Issues

 * 131 NUnit test adapter not running all tests - only on VS2015
 * 135 Upgrade TestEngine to 3.2.1
 * 162 Visual Studio 15 support
 * 163 No source location when inheriting test methods from base test fixture
 * 174 Clarify that NUnit v2 tests are not discovered by v3 adapter
 * 176 More Information link in vsix broken

#### NUnit3 Test Adapter for Visual Studio - Version 3.0 - April 2, 2016

##### Features

 * This is the final production release of the 3.0 adapter. It continues to use the 3.0.1 release of the NUnit TestEngine.

 * The adapter now uses a `.runsettings` file for all optional settings. Registry entries used in the CTP releases are no longer used.

##### Resolved Issues

 * 49 Need a way to specify test settings
 * 52 Having ApartmentAttribute on both classes and methods causes test runner to hang
 * 85 Failure to run tests under vstest.console from VS2015
 * 92 Provide option to run in parallel for parallelized tests
 * 120 The ability to set the LevelOfParallelism attribute through the VS adapter
 * 153 TFS Filter that matches no names runs all tests

#### NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 9 - April 2, 2016

##### Features

 * The adapter continues to use the 3.0.1 release of the NUnit TestEngine.

##### Resolved Issues

 * 2 CI Build
 * 34 Identifying Non-Primitive Parameterized Inputs in Adapter vs Console
 * 50 NuGet version install script doesn't work with VS 2015
 * 66 Build the adapter in AppVeyor
 * 84 CopyLocal=False is an issue in a specific use case
 * 94 More Information Link in Adapter Broken
 * 96 Working directory is set to VS TestWindow extension directory
 * 102 Package VS2012 assemblies as a private NuGet Package
 * 104 Can't overload async/await methods with NUnit Test Adapter
 * 106 Explicit tests appear as warnings in NUnit 3.0
 * 109 NUnit 2 tests are detected as errors
 * 112 Test adapter fails to load an assembly that references a class from NUnit.Framework but contains no tests
 * 117 Version 3.0.8.0 as NuGet package only. No tests detected in Visual Studio 2015
 * 118 Corrupted ignore.addins file in installation

#### NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 8 - December 2, 2015

##### Features

 * The adapter now uses the 3.0.1 release of the NUnit TestEngine.

##### Resolved Issues

 * 81 Cannot run tests with '>' in name
 * 86 Generic Test Fixtures are not getting triggered
 * 88 Upgrade adapter to use NUnit 3.0.1

#### NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 7 - November 16, 2015

##### Features

 * The adapter now uses the released NUnit 3.0 TestEngine.

##### Resolved Issues

 * 75 Update adapter to use final release of NUnit 3.0 

#### NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 6 - November 10, 2015

##### Features

 * This release continues to use the NUnit RC 2 Engine.

##### Resolved Issues

 * 14 NUnit Adapter throws System.Reflection.TargetInvocationException, even if the solution build is OK
 * 56 Exception System.Reflection.TargetInvocationException after NUnit 3.0.0-beta-5 upgrade
 * 68 NUnit3TestExecutor.MakeTestFilter does not create valid xml
 * 69 NUnit 3.0.0-rc-2 : System.Reflection.TargetInvocationException
 * 70 NUnit3TestExecutor.MakeTestFilter creates element not handled by NUnit.Framework.Internal.TestFilter 

#### NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 5 - November 9, 2015

##### Features

 * This release uses the NUnit RC 2 Engine.

##### Resolved Issues

 * 27 Async void methods do not show up as not runnable
 * 43 Remove Wrappers for Engine Classes
 * 45 Remove workaround for tests not sending events
 * 53 Replace core engine
 * 57 Confusing message when an NUnit V2 test is detected

#### NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 4 - July 20, 2015

##### Features

 * This release continues to use the NUnit 3.0 beta-2 engine but is nevertheless able to run tests that reference NUnit 3.0 beta-3 framework.

 * When a debugger is attached, only a single worker thread is used to run tests.

 * The adapter now compensates for the fact that NUnit does not send results for tests that were skipped due to an attribute on the fixture by generating those results itself.

##### Resolved Issues

 * 16 Adapter does not detect C++/CLI assemblies
 * 26 Ignored test case does not show up as ignored
 * 33 Inconsistent display behavior in Test Explorer
 * 36 Option to set number of worker threads

#### NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 3 - May 22, 2015

##### Features

This release was issued to correct a problem with locking of assemblies in ctp-2.

##### Resolved Issues

 * 29 Latest test adapter locking dlls

#### NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 2 - May 16, 2015

##### Features

 * The adapter now uses the new nunit.core.engine to load and run tests, eliminating ad-hoc code that worked directly with the framework. This will allow us to much greater flexibility in the future.

 * The adapter has been upgraded to use the beta-2 release of the NUnit core engine. Because the API has changed from beta-1, the adapter can only run tests built against the beta-2 release of NUnit.

##### Resolved Issues

 * 13 Adapter will not load as a NuGet package
 * 17 Can't read app.config settings within test methods
 * 18 Separate NUnit3TestDemo from NUnitTestAdapter solution
 * 19 Use core engine
 * 20 Upgrade NUnit to beta-2

#### NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 1 - April 6, 2015

##### Features

 * Initial release of the test adapter using NUnit 3.0. Note that the adapter may **not** be used to run tests written against earlier versions of NUnit. The original adapter is still available for that purpose and both adapters may be installed if necessary.

#### NUnit Test Adapter for Visual Studio - Version 2.0 - April 1, 2015

##### Features

 * Tested for up to VS2015 Pre-release CTP 6
 * Updated to use NUnit 2.6.4
 * Adapter does not try to discover tests if the nunit.framework version is 3.0 or greater

##### Bug Fixes

 * #61 Confusing NUnit version message made clearer
 * #62 Adapter uses shadowcopy setting in discoverer but not in the executor

#### NUnit Test Adapter for Visual Studio (RTM) - Version 1.2 - September 17, 2014

##### Features

 * Tested for up to VS2013 Update 3
 * Bugs 39 and 40 was inability to run under VS2012. This is now fixed.

##### Bug Fixes

 * #24 Long-running tests ignored
 * #34 Adapter causes ArgumentException to be thrown by Microsoft logger proxy's SendMessage method
 * #37 TestExecution throws Exception System.InvalidOperationException in TFS Build
 * #38 NUnit only accepts absolute paths to test assembly
 * #39 VSTest unable to find NUnit tests since 1.1.0.0
 * #40 NUnit version 1.1.0.0 is broken with test class which ran under 1.0.0.0

#### NUnit Test Adapter for Visual Studio (RTM) - Version 1.1 - April 26, 2014

##### Features

 * Support for NUnit 2.6.3
 * Tested for up to VS2013 Update 2 RC
 * Shadow copy now disabled by default, see issue #7 Unable to disable shadow copy.
 * Registry settings added for some customization options, see Tips and Tricks
 * All code moved to github

##### Bug Fixes

 * #13 Category attribute not working with TFS test case filter
 * #21 Xamarin.iOS NUnit project causes adapter to throw

#### NUnit Test Adapter for Visual Studio (RTM) - Version 1.0 - September 12, 2013

##### Features

 * This is the release version 1.0 of the test adapter.

##### Bug Fixes

 * #1208148 The test result output node is not shown for debug/trace statements

#### NUnit Test Adapter for Visual Studio (RC) - Version 0.97 - September 12, 2013

##### Features

 * This is the release candidate for version 1.0 of the test adapter.

##### Bug Fixes

 * #1208161 NUnit Test Adapter runs [Explicit] unit tests in TFS Build
 * #1210536 No Source Available for Async Tests
 * #1165188 Clicking "Run Selected Tests" doesn't show Trace.WriteLine() output

#### NUnit Test Adapter for Visual Studio (Beta 6) - Version 0.96 - June 28, 2013

##### Features

 * Support for Visual Studio 2013 Preview

##### Bug Fixes

 * #1189268 Profile a test will crash with exception

#### NUnit Test Adapter for Visual Studio (Beta 5) - Version 0.95.2 - June 7, 2013

##### Bug Fixes

 * #1188000, adapter dont work with solutions with only .net 2.0/3.5 project

#### NUnit Test Adapter for Visual Studio (Beta 5) - Version 0.95.1 Hotfix- May 28, 2013

##### Bug Fixes

 * Hotfix for debug issue

#### NUnit Test Adapter for Visual Studio (Beta 5) - Version 0.95 - May 10, 2013

##### Features

 * #1174925 Add support for installing the adapter from NuGet

##### Bug Fixes

 * #1155617 Grouping by class name in VS 2012 doesn't work
 * #1165359 Exception after building Coded UI test
 * #1116747 vstest.executionengine.x86.exe does not terminate
 * #1093178 Eliminate unnecessary files from VSIX

#### NUnit Test Adapter for Visual Studio (Beta 4) - Version 0.94 - December 22, 2012

##### Features

 * Works with Visual Studio 2012 Update 1 as well as the RTM.
 * Supports filtering and sorting tests by Traits under Update 1.
 * Supports use of standard filter expressions when running under TFS Update 1.
 * NUnit Categories specified on the fixture class are now recognized and honored. 

##### Bug Fixes

 * 1074891 Can't test multiple assemblies referencing different NUnit versions
 * 1075893 Test execution fails if solution contains native C++ project
 * 1076012 No source information found for async test methods
 * 1087629 TestFixture Category not being recognised as traits in VS2012 update 1
 * 1091020 Adapter doesn't support TFS Build traits/test case filtering 

#### NUnit Test Adapter for Visual Studio (Beta 3-2) - Version 0.93.2 - November 2, 2012

##### Bug Fixes

 * 1074544 Failures in Test Discovery not reporting sufficient information 

#### NUnit Test Adapter for Visual Studio (Beta 3-1) - Version 0.93.1 - October 26, 2012

##### Bug Fixes

 * 1072150 NUnit adapter 0.93 won't run selected tests 

#### NUnit Test Adapter for Visual Studio (Beta 3) - Version 0.93 - October 24, 2012

##### Features

 * Works with Visual Studio 2012 RTM. Some features require the November CTP update.
 * The adapter now uses NUnit 2.6.2. Among other things, this allows us to support async test methods. See the NUnit Release Notes for more info.
 * Source file and line number can now be found for test cases that have an alternate name set.
 * Console output from tests is now displayed in the Visual Studio Output window.
 * TestFixtureSetUp and TestFixtureTearDown errors are now displayed in the Output window.
 * The caret line (------^) is no longer displayed in the IDE since it depends on use of a fixed font.
 * Tests may now be grouped and filtered by Category (only under the November CTP update for VS2012). 

##### Bug Fixes

 * 1021144 Text output from tests not displayed in Visual Studio IDE
 * 1033623 Not possible to include or exclude tests based on [Category] attribute Released
 * 1040779 Null reference exception on generic test fixtures
 * 1064620 Support async test methods
 * 1065209 Should call both RecordEnd and RecordResult at end of a test
 * 1065212 Upgrade NUnit to 2.6.2
 * 1065223 Error messages assume a fixed font, but don't get one
 * 1065225 No display for TestFixtureSetUp/TearDown or SetUpFixture errors
 * 1065254 Cannot open test from Test Explorer for tests in a Parameterized Test Fixture
 * 1065306 Generic Fixtures aren't discovered.
 * 1066393 Unable to display source for test cases with an alternate name set
 * 1066518 Executed fast test appears in Not Run category in Test Explorer 

#### NUnit Test Adapter for Visual Studio (Beta 2) - Version 0.92 - May 3, 2012

##### Features

 * Works with Visual Studio 2012 Release Candidate
 * Uses NUnit 2.6 

##### Bug Fixes

 * 992837 Unable to Debug using VS Test Adapter
 * 994146 Can't run tests under .NET 2.0/3.5 

#### NUnit Test Adapter for Visual Studio (Beta 1) - Version 0.91 - February 29, 2012

##### Features

 * Built against Visual Studio 11 Beta 1
 * Uses NUnit 2.6 

#### NUnit Test Adapter for Visual Studio (Alpha) - Version 0.90 - February 21, 2012

##### Features

 * First release of the test adapter. Compatible with the Visual Studio 11 Developer Preview.
 * Uses NUnit 2.6. 
