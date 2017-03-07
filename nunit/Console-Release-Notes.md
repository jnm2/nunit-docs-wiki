###NUnit Console 3.6.1 - March 6, 2017

####Engine

 * This hotfix release addresses a race condition in the Engine that caused
   tests to intermittently fail.

####Issues Resolved

 * 168 Intermittent errors while running tests after updating to 3.6


###NUnit Console 3.6 - January 14, 2017

####Console Runner

 * Added command line option --skipnontestassemblies to skip assemblies that do
   not contain tests without raising an error and to skip assemblies that contain
   the NUnit.Framework.NonTestAssemblyAttribute.
 * Messages from the new Multiple Assert blocks will be displayed individually
 * Warnings from the new Warn.If, Warn.Unless and Assert.Warn are now displayed

####Engine

 * NUnit agents now monitor the running engine process and will terminate themselves
   if the parent runner process is killed or dies

####Issues Resolved

 * 16 NUnit Engine Tests fail if not run from test directory
 * 18 Invalid file type is shown in XML as type="Assembly"
 * 23 In nunit3-console you cannot pass parameters containing ';' because they always get split
 * 37 NUnit 3 console should produce xml events for ITestEventListener which contain
      unique id in the scope of all test agents for NUnit 2 tests
 * 58 System.Configuration.ConfigurationErrorsException thrown in multiple domain mode.
 * 62 NUnit3 Fails on DLL with no Tests, Unlike NUnit2
 * 100 Class NUnit.Engine.Services.ResultWriters.Tests.SchemaValidator is never used
 * 101 Method NUnit.Options.OptionSet.Unprocessed always returns "false"
 * 104 Type of variable enumerated in 'foreach' is not guaranteed to be castable
 * 110 Writability check could give a friendlier message.
 * 113 Add task descriptions to Build.cake
 * 127 Modify console runner to display multiple assert information
 * 128 Terminate agent if main process has terminated
 * 133 NUnit downloadable packages zip file naming is confusing and non-intuitive
 * 136 Handle early termination of multiple assert block
 * 138 Report Warnings in console runner
 * 145 MasterTestRunner.RunAsync no longer provides start-run and test-run events
 * 151 Unexpected behaviour from --framework flag
 * 153 Remove some settings used by the engine
 * 156 Use high-quality icon for nuspecs
 * 157 Fix Detection of invalid framework when --inprocess
 * 159 Update extension versions in the NuSpec Files

<h3>Earlier Releases</h3>

<ul>
<li>Release Notes for [[NUnit 2.9.1 through 3.5|Release-Notes]].
<li>Release Notes for <a href="http://www.nunit.org/?p=releaseNotes&r=2.6.4">NUnit 2.6 through 2.6.4</a>
<li>Release Notes for <a href="http://www.nunit.org/?p=releaseNotes&r=2.5.10">NUnit 2.5 through 2.5.10</a>
<li>Release Notes for <a href="http://www.nunit.org/?p=releaseNotes&r=2.4.8">NUnit 2.4 through 2.4.8</a>
<li>Release Notes for <a href="http://www.nunit.org/?p=releaseNotes&r=2.2.10">NUnit 2.0 through 2.2.10</a>
</ul>
