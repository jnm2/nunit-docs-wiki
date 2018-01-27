### NUnit 3.8 - January 27, 2018

This release includes several fixes when unloading AppDomains and better error reporting. The
aggregate NuGet packages also include updated versions of several extensions.

#### Issues Resolved

 * [6](https://github.com/nunit/nunit-console/issues/6) TypeLoadException in nunit3-console 3.0.1
 * [93](https://github.com/nunit/nunit-console/issues/93) Update Readme with information about the NuGet packages
 * [111](https://github.com/nunit/nunit-console/issues/111) Provide better info when AppDomain won't unload
 * [116](https://github.com/nunit/nunit-console/issues/116) NUnit 3.5.0 defaults to single agent process when using an nunit project file
 * [191](https://github.com/nunit/nunit-console/issues/191) Exception encountered unloading AppDomain
 * [228](https://github.com/nunit/nunit-console/issues/228) System.Reflection.TargetInvocationException with nunit3-console --debug on Mono
 * [246](https://github.com/nunit/nunit-console/issues/246) No way to specify app.config with console runner
 * [256](https://github.com/nunit/nunit-console/issues/256) Rewrite ConsoleRunnerTests.ThrowsNUnitEngineExceptionWhenTestResultsAreNotWriteable()
 * [259](https://github.com/nunit/nunit-console/issues/259) NUnit3 agent hangs after encountering an "CannotUnloadAppDomainException"
 * [262](https://github.com/nunit/nunit-console/issues/262) Transform file existence check should check current directory instead of WorkDirectory
 * [267](https://github.com/nunit/nunit-console/issues/267) Fix possible NRE
 * [273](https://github.com/nunit/nunit-console/issues/273) Insufficient error handling message in ProcessRunner -> RunTests method
 * [275](https://github.com/nunit/nunit-console/issues/275) Integrate chocolatey packages with build script
 * [284](https://github.com/nunit/nunit-console/issues/284) NUnit3: An exception occured in the driver while loading tests...   bei NUnit.Engine.Runners.ProcessRunner.RunTests(ITestEventListener listener, TestFilter filter)
 * [285](https://github.com/nunit/nunit-console/issues/285) ColorConsoleWriter.WriteLabel causes NullReferenceException
 * [289](https://github.com/nunit/nunit-console/issues/289) Warnings not displayed
 * [298](https://github.com/nunit/nunit-console/issues/298) Invalid --framework option throws exception
 * [300](https://github.com/nunit/nunit-console/issues/300) Agents do not respect the Console WORK parameter when writing log file
 * [304](https://github.com/nunit/nunit-console/issues/304) Catch agent debugger launch exceptions, and improve agent crash handling
 * [309](https://github.com/nunit/nunit-console/issues/309) No driver found if framework assembly reference has uppercase characters
 * [314](https://github.com/nunit/nunit-console/issues/314) Update NUnit.Extension.VSProjectLoader to 3.7.0
 * [318](https://github.com/nunit/nunit-console/issues/318) Update NUnit.Extension.TeamCityEventListener to 1.0.3
 * [320](https://github.com/nunit/nunit-console/issues/320) Return error code -5 when AppDomain fails to unload
 * [323](https://github.com/nunit/nunit-console/issues/323) Assertion should not be ordered in AgentDatabaseTests
 * [343](https://github.com/nunit/nunit-console/issues/343) Superfluous unload error shown in console
 * [349](https://github.com/nunit/nunit-console/issues/349) Get all TestEngine tests running under NUnitAdapter apart from those .
 * [350](https://github.com/nunit/nunit-console/issues/350) Invalid assemblies no longer give an error message
 * [355](https://github.com/nunit/nunit-console/issues/355) NuGet package links to outdated license

### NUnit 3.7 - July 13, 2017

#### Engine

 * Creates a .NET Standard version of the engine for use in the Visual Studio Adapter
 * Fixes several issues that caused the runner to exit with a SocketException
#### Issues Resolved

 * [10](https://github.com/nunit/nunit-console/issues/10) Create a .NET Standard version of the Engine
 * [11](https://github.com/nunit/nunit-console/issues/11) insufficient info on driver reflection exception
 * [12](https://github.com/nunit/nunit-console/issues/12) Upgrade Cake build to latest version
 * [24](https://github.com/nunit/nunit-console/issues/24) Update --labels switch with option to show real-time pass/fail results in console runner
 * [31](https://github.com/nunit/nunit-console/issues/31) Nunit 3.4.1 NUnit.Engine.Runners
 * [72](https://github.com/nunit/nunit-console/issues/72) TestContext.Progress.Write writes new line
 * [82](https://github.com/nunit/nunit-console/issues/82) Remove unused repository paths from repositories.config
 * [99](https://github.com/nunit/nunit-console/issues/99) Remove unused --verbose and --full command line options
 * [126](https://github.com/nunit/nunit-console/issues/126) Resolve differences between NUnit Console and NUnitLite implementations of @filename
 * [162](https://github.com/nunit/nunit-console/issues/162) Add namespace keyword to Test Selection Language
 * [171](https://github.com/nunit/nunit-console/issues/171) Socket Exception when stopping Remote Agent
 * [172](https://github.com/nunit/nunit-console/issues/172) Limit Language level to C#6
 * [193](https://github.com/nunit/nunit-console/issues/193) Settings are stored with invariant culture but retrieved with CurrentCulture
 * [194](https://github.com/nunit/nunit-console/issues/194) Better logging or error handling in SettingsStore.SaveSettings
 * [196](https://github.com/nunit/nunit-console/issues/196) Allow comments in @FILE files
 * [200](https://github.com/nunit/nunit-console/issues/200) Remove obsolete warnings from build script
 * [206](https://github.com/nunit/nunit-console/issues/206) Remove reference to removed noxml option
 * [207](https://github.com/nunit/nunit-console/issues/207)  Create Chocolatey package(s) for the console
 * [208](https://github.com/nunit/nunit-console/issues/208) Explore flags test update
 * [213](https://github.com/nunit/nunit-console/issues/213) Master build failing after merging .NET Standard Engine
 * [216](https://github.com/nunit/nunit-console/issues/216) Compiling mock-assembly in Visual Studio 2017 fails
 * [217](https://github.com/nunit/nunit-console/issues/217) NUnit .NET Standard NuGet package missing some values
 * [219](https://github.com/nunit/nunit-console/issues/219) Runtime.Remoting.RemotingException in NUnit.Engine.Runners.ProcessRunner.Dispose
 * [221](https://github.com/nunit/nunit-console/issues/221) Added missing nuget package info
 * [222](https://github.com/nunit/nunit-console/issues/222) Improve missing agent error message
 * [225](https://github.com/nunit/nunit-console/issues/225) SocketException thrown by nunit3-console.exe --explore option
 * [248](https://github.com/nunit/nunit-console/issues/248) Agent TestEngine contains duplicate services
 * [252](https://github.com/nunit/nunit-console/issues/252) Console crashes when specifying both format and transform for result
 * [254](https://github.com/nunit/nunit-console/issues/254) Correct misprint ".con" -> ".com"

### NUnit Console 3.6.1 - March 6, 2017

#### Engine

 * This hotfix release addresses a race condition in the Engine that caused
   tests to intermittently fail.

#### Issues Resolved

 * [168](https://github.com/nunit/docs/issues/168) Intermittent errors while running tests after updating to 3.6


### NUnit Console 3.6 - January 14, 2017

#### Console Runner

 * Added command line option --skipnontestassemblies to skip assemblies that do
   not contain tests without raising an error and to skip assemblies that contain
   the NUnit.Framework.NonTestAssemblyAttribute.
 * Messages from the new Multiple Assert blocks will be displayed individually
 * Warnings from the new Warn.If, Warn.Unless and Assert.Warn are now displayed

#### Engine

 * NUnit agents now monitor the running engine process and will terminate themselves
   if the parent runner process is killed or dies

#### Issues Resolved

 * [16](https://github.com/nunit/nunit-console/issues/16) NUnit Engine Tests fail if not run from test directory
 * [18](https://github.com/nunit/nunit-console/issues/18) Invalid file type is shown in XML as type="Assembly"
 * [23](https://github.com/nunit/nunit-console/issues/23) In nunit3-console you cannot pass parameters containing ';' because they always get split
 * [37](https://github.com/nunit/nunit-console/issues/37) NUnit 3 console should produce xml events for ITestEventListener which contain
      unique id in the scope of all test agents for NUnit 2 tests
 * [58](https://github.com/nunit/nunit-console/issues/58) System.Configuration.ConfigurationErrorsException thrown in multiple domain mode.
 * [62](https://github.com/nunit/nunit-console/issues/62) NUnit3 Fails on DLL with no Tests, Unlike NUnit2
 * [100](https://github.com/nunit/nunit-console/issues/100) Class NUnit.Engine.Services.ResultWriters.Tests.SchemaValidator is never used
 * [101](https://github.com/nunit/nunit-console/issues/101) Method NUnit.Options.OptionSet.Unprocessed always returns "false"
 * [104](https://github.com/nunit/nunit-console/issues/104) Type of variable enumerated in 'foreach' is not guaranteed to be castable
 * [110](https://github.com/nunit/nunit-console/issues/110) Writability check could give a friendlier message.
 * [113](https://github.com/nunit/nunit-console/issues/113) Add task descriptions to Build.cake
 * [127](https://github.com/nunit/nunit-console/issues/127) Modify console runner to display multiple assert information
 * [128](https://github.com/nunit/nunit-console/issues/128) Terminate agent if main process has terminated
 * [133](https://github.com/nunit/nunit-console/issues/133) NUnit downloadable packages zip file naming is confusing and non-intuitive
 * [136](https://github.com/nunit/nunit-console/issues/136) Handle early termination of multiple assert block
 * [138](https://github.com/nunit/nunit-console/issues/138) Report Warnings in console runner
 * [145](https://github.com/nunit/nunit-console/issues/145) MasterTestRunner.RunAsync no longer provides start-run and test-run events
 * [151](https://github.com/nunit/nunit-console/issues/151) Unexpected behaviour from --framework flag
 * [153](https://github.com/nunit/nunit-console/issues/153) Remove some settings used by the engine
 * [156](https://github.com/nunit/nunit-console/issues/156) Use high-quality icon for nuspecs
 * [157](https://github.com/nunit/nunit-console/issues/157) Fix Detection of invalid framework when --inprocess
 * [159](https://github.com/nunit/nunit-console/issues/159) Update extension versions in the NuSpec Files

### Earlier Releases
 * Release Notes for [[NUnit 2.9.1 through 3.5|Pre-3.5-Release-Notes]].
 * Release Notes for [NUnit 2.6 through 2.6.4](http://www.nunit.org/?p=releaseNotes&r=2.6.4)
 * Release Notes for [NUnit 2.5 through 2.5.10](http://www.nunit.org/?p=releaseNotes&r=2.5.10)
 * Release Notes for [NUnit 2.4 through 2.4.8](http://www.nunit.org/?p=releaseNotes&r=2.4.8)
 * Release Notes for [NUnit 2.0 through 2.2.10](http://www.nunit.org/?p=releaseNotes&r=2.2.10)
