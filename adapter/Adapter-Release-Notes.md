####NUnit3 Test Adapter for Visual Studio - Version 3.0 - April 2, 2016

#####Features

 * This is the final production release of the 3.0 adapter. It continues to use the 3.0.1 release of the NUnit TestEngine.

 * The adapter now uses a `.runsettings` file for all optional settings. Registry entries used in the CTP releases are no longer used.

#####Resolved Issues

 * 49 Need a way to specify test settings
 * 52 Having ApartmentAttribute on both classes and methods causes test runner to hang
 * 85 Failure to run tests under vstest.console from VS2015
 * 92 Provide option to run in parallel for paralellized tests
 * 120 The ability to set the LevelOfParallelism attribute through the VS adapter
 * 153 TFS Filter that matches no names runs all tests

####NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 9 - April 2, 2016

#####Features

 * The adapter continues to use the 3.0.1 release of the NUnit TestEngine.

#####Resolved Issues

 * 2 CI Build
 * 34 Identifying Non-Primitive Parameterized Inputs in Adapter vs Console
 * 50 Nuget version install script doesn't work with VS 2015
 * 66 Build the adapter in AppVeyor
 * 84 CopyLocal=False is an issue in a specific use case
 * 94 More Information Link in Adapter Broken
 * 96 Working directory is set to VS TestWindow extension directory
 * 102 Package VS2012 assemblies as a private NuGet Package
 * 104 Can't overload async/await methods with NUnit Test Adapter
 * 106 Explicit tests appear as warnings in NUnit 3.0
 * 109 NUnit 2 tests are detected as errors
 * 112 Test adapter fails to load an assembly that references a class from NUnit.Framework but contains no tests
 * 117 Version 3.0.8.0 as nuget package only. No tests detected in Visual Studio 2015
 * 118 Corrupted ignore.addins file in installation

####NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 8 - December 2, 2015

#####Features

 * The adapter now uses the 3.0.1 release of the NUnit TestEngine.

#####Resolved Issues

 * 81 Cannot run tests with '>' in name
 * 86 Generic Test Fixtures are not getting triggered
 * 88 Upgrade adapter to use NUnit 3.0.1

####NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 7 - November 16, 2015

#####Features

 * The adapter now uses the released NUnit 3.0 TestEngine.

#####Resolved Issues

 * 75 Update adapter to use final release of NUnit 3.0 

####NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 6 - November 10, 2015

#####Features

 * This release continues to use the NUnit RC 2 Engine.

#####Resolved Issues

 * 14 NUnit Adapter throws System.Reflection.TargetInvocationException, even if the solution build is OK
 * 56 Exception System.Reflection.TargetInvocationException after NUnit 3.0.0-beta-5 upgrade
 * 68 NUnit3TestExecutor.MakeTestFilter does not create valid xml
 * 69 Nunit 3.0.0-rc-2 : System.Reflection.TargetInvocationException
 * 70 NUnit3TestExecutor.MakeTestFilter creates element not handled by NUnit.Framework.Internal.TestFilter 

####NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 5 - November 9, 2015

#####Features

 * This release uses the NUnit RC 2 Engine.

#####Resolved Issues

 * 27 Async void methods do not show up as not runnable
 * 43 Remove Wrappers for Engine Classes
 * 45 Remove workaround for tests not sending events
 * 53 Replace core engine
 * 57 Confusing message when an NUnit V2 test is detected

####NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 4 - July 20, 2015

#####Features

 * This release continues to use the NUnit 3.0 beta-2 engine but is nevertheless able to run tests that reference NUnit 3.0 beta-3 framework.

 * When a debugger is attached, only a single worker thread is used to run tests.

 * The adapter now compensates for the fact that NUnit does not send results for tests that were skipped due to an attribute on the fixture by generating those results itself.

#####Resolved Issues

 * 16 Adapter does not detect C++/CLI assemblies
 * 26 Ignored test case does not show up as ignored
 * 33 Inconsistent display behavior in Test Explorer
 * 36 Option to set number of worker threads

####NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 3 - May 22, 2015

#####Features

This release was issued to correct a problem with locking of assemblies in ctp-2.

#####Resolved Issues

 * 29 Latest test adapter locking dlls

####NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 2 - May 16, 2015

#####Features

 * The adapter now uses the new nunit.core.engine to load and run tests, eliminating adhoc code that worked directly with the framework. This will allow us to much greater flexibility in the future.

 * The adapter has been upgraded to use the beta-2 release of the NUnit core engine. Because the API has changed from beta-1, the adapter can only run tests built against the beta-2 release of NUnit.

#####Resolved Issues

 * 13 Adapter will not load as a NuGet package
 * 17 Can't read app.config settings within test methods
 * 18 Separate NUnit3TestDemo from NUnitTestAdapter solution
 * 19 Use core engine
 * 20 Upgrade NUnit to beta-2

####NUnit3 Test Adapter for Visual Studio - Version 3.0 CTP 1 - April 6, 2015

#####Features

 * Initial release of the test adapter using NUnit 3.0. Note that the adapter may <b>not</b> be used to run tests written against earlier versions of NUnit. The original adapter is still available for that purpose and both adapters may be installed if necessary.

#####Earlier Releases

 * Release Notes for <a href="http://www.nunit.org/?p=vsTestAdapterReleaseNotes&r=2.6.4">earlier versions of the adapter</a>

