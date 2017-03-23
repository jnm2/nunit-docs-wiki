### NUnit 3.6.1 - February 26, 2017

This is a hotfix release of the framework that addresses critical issues found in
the 3.6 release.

#### Issues Resolved

 * 1962 A Theory with no data passes
 * 1986 NUnitLite ignores --workers option
 * 1994 NUnitLite runner crashing when --trace is specified
 * 2017 Two NUnit project's tests fail on systems with comma decimal mark settings
 * 2043 Regression in 3.6.0 when catching AssertionException

### NUnit 3.6 - January 9, 2017

This release of the framework no longer includes builds for Compact Framework or for SilverLight, but adds a .NET Standard 1.6 build. If anyone still using Compact Framework or SilverLight and would like to continue development on those versions of the framework, please contact the NUnit team.

#### Framework

 * .NET Standard 1.6 is now supported
 * Adds support for Multiple Assert blocks
 * Added the --params option to NUnitLite
 * Theories now support Nullable enums
 * Improved assert error messages to help differentiate differences in values
 * Added warnings with Warn.If(), Warn.Unless() and Assert.Warn()
 * Enabled Path, File and Directory Asserts/Contraints for .NET Core testing
 * Added NonTestAssemblyAttribute for use by third-party developers to indicate that their assemblies reference the NUnit framework, but do not contain tests

#### Issues Resolved

 * 406 Warning-level Assertions
 * 890 Allow file references anywhere in the command line.
 * 1380 Appveyor Failures when branch name is too long
 * 1589 Split the nunit repository into multiple repositories
 * 1599 Move Compact Framework to separate project
 * 1601 Move Silverlight to a separate project
 * 1609 Upgrade Cake build to latest version
 * 1661 Create .NET Standard Framework Build
 * 1668 Need implementation-independent way to test number of items in a collection
 * 1743 Provide multiple results for a test case in the XML output
 * 1758 No direct inverse for Contains.Key
 * 1765 TestCaseSourceAttribute constructor for method with parameters
 * 1802 Design Multiple Assert syntax as seen by users
 * 1808 Disambiguate error messages from EqualConstraint
 * 1811 Build.ps1 fails if spaces in path
 * 1823 Remove engine nuspecs and old global.json
 * 1827 Remove unused repository paths from repositories.config
 * 1828 Add Retry for failed tests only
 * 1829 NUnitLite accepts --params option but does not make any use of it.
 * 1836 Support nullable enums in Theories
 * 1837 [Request] AfterContraint to support more readable usage
 * 1840 Remove SL and CF #Defined source
 * 1866 [Request] More readable way to set polling interval in After constraint
 * 1870 EqualConstraint result failure message for DateTime doesn't show sufficient resolution
 * 1872 Parameterized method being called with no parameter
 * 1876 What should we do about Env.cs
 * 1880 AttributeUsage for various Attributes
 * 1889 Modify nunitlite to display multiple assert information
 * 1891 TestContext.Progress and TestContext.Error silently drop text that is not properly XML encoded
 * 1901 Make nunitlite-runner Prefer32Bit option consistent across Debug/Release
 * 1904 Add .NET Standard 1.6 Dependencies to the Nuspec Files
 * 1907 Handle early termination of multiple assert block
 * 1911 Changing misleading comment that implies that every ICollection<T> is a list
 * 1912 Add new warning status and result state
 * 1913 Report Warnings in NUnitLite
 * 1914 Extra AssertionResult entries in TestResults
 * 1915 Enable Path, File and Directory Assert/Constraints in the .NET Standard Build
 * 1917 Use of IsolatedContext breaks tests in user-created AppDomain
 * 1924 Run tests using the NUnit Console Runner
 * 1929 Rename zip and remove source zip
 * 1933 Tests should pass if test case source provides 0 test cases
 * 1941 Use dictionary-based property for test run parameters
 * 1945 Use high-quality icon for nuspecs
 * 1947 Add NonTestAssemblyAttribute
 * 1954 Change Error Message for Assert.Equals
 * 1960 Typo fixes
 * 1966 Xamarin Runner cannot reference NUnit NuGet Package

<h3>Earlier Releases</h3>

<ul>
<li>Release Notes for [[NUnit 2.9.1 through 3.5|Pre-3.5-Release-Notes]]
<li>Release Notes for <a href="http://www.nunit.org/?p=releaseNotes&r=2.6.4">NUnit 2.6 through 2.6.4</a>
<li>Release Notes for <a href="http://www.nunit.org/?p=releaseNotes&r=2.5.10">NUnit 2.5 through 2.5.10</a>
<li>Release Notes for <a href="http://www.nunit.org/?p=releaseNotes&r=2.4.8">NUnit 2.4 through 2.4.8</a>
<li>Release Notes for <a href="http://www.nunit.org/?p=releaseNotes&r=2.2.10">NUnit 2.0 through 2.2.10</a>
</ul>
