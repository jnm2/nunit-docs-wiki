This page lists features present in NUnit 2.6, which are either removed in NUnit 3.0 or have had their behavior modified in a way that will break existing code.

######Attributes

|            Name              |          Notes                                        |
|------------------------------|-------------------------------------------------------|
| ExpectedExceptionAttribute   | No longer supported. Use `Assert.Throws` or `Assert.That`. |
| IgnoreAttribute              | The reason is now mandatory |
| RequiredAddinAttribute       | No longer supported. |
| RequiresMTAAttribute         | Deprecated. Use `ApartmentAttribute`                    |
| RequiresSTAAttribute         | Deprecated. Use `ApartmentAttribute`                    |
| SuiteAttribute               | No longer supported. |
| System.MTAThreadAttribute    | No longer treated as `RequiresMTAAttribute`             |
| System.STAThreadAttribute    | No longer treated as `RequiresSTAAttribute`             | 
| TearDown and OneTimeTearDown | There is a change to the logic by which teardown methods are called. See [[SetUp and TearDown Changes]] for details. |
| TestCaseAttribute            | Named parameter `Result=` is no longer supported. Use `ExpectedResult=`. Named parameter `Ignore=` now takes a string, giving the reason for ignoring the test.|
| TestCaseSourceAttribute      | The attribute forms using a string argument to refer to the data source must now use only static fields, properties or methods. |
| TestFixtureAttribute         | Named parameter `Ignore=` now takes a string, giving the reason for ignoring the test. |
| TestFixtureSetUpAttribute    | Deprecated. Use `OneTimeSetUpAttribute`.  |
| TestFixtureTearDownAttribute | Deprecated. Use `OneTimeTearDownAttribute`.  |
| ValueSourceAttribute         | The source name of the data source must now use only static fields, properties or  methods. |

######Assertions and Constraints

|          Feature                 |          Notes                                        |
|----------------------------------|-------------------------------------------------------|
| Assert.IsNullOrEmpty             | No longer supported. Use `Assert.That(..., Is.Null.Or.Empty)` |
| Assert.IsNotNullOrEmpty          | No longer supported. Use `Assert.That(..., Is.Not.Null.And.Not.Empty)` |
| Is.InstanceOfType                | No longer supported. Use `Is.InstanceOf`                    |
| Is.StringStarting                | Deprecated. Use `Does.StartWith` |
| Is.StringContaining              | Deprecated. Use `Does.Contain` |
| Is.StringEnding                  | Deprecated. Use `Does.EndWith` |
| Is.StringMatching                | Deprecated. Use `Does.Match` |
| NullOrEmptyStringConstraint      | No longer supported. See `Assert.IsNullOrEmpty` above   |
| SubDirectoryContainsConstraint   | No longer supported. Various alternatives are available.    |
| Text.All                         | No longer supported. Use `Does.All` |
| Text.Contains                    | No longer supported. Use `Does.Contain` or `Contains.Substring` |
| Text.DoesNotContain              | No longer supported. Use `Does.Not.Contain` |
| Text.StartsWith                  | No longer supported. Use `Does.StartWith` |
| Text.DoesNotStartWith            | No longer supported. Use `Does.Not.StartWith` |
| Text.EndsWith                    | No longer supported. Use `Does.EndWith` |
| Text.DoesNotEndWith              | No longer supported. Use `Does.Not.EndWith` |
| Text.Matches                     | No longer supported. Use `Does.Match` |
| Text.DoesNotMatch                | No longer supported. Use `Does.Not.Match` |

######Other Framework Features

|      Feature       |          Notes                                        |
|--------------------|-------------------------------------------------------|
| Addins             | No longer supported. See [[Addin Replacement in the Framework]]. |
| CurrentDirectory   | No longer set to the directory containing the test assembly. Use `TestContext.CurrentContext.TestDirectory` to locate that directory. |
| NUnitLite          | NUnitLite executable tests must now reference nunit.framework in addition to nunitlite. |
| SetUpFixture       | Now uses `OneTimeSetUpAttribute` and `OneTimeTearDownAttribute` to designate higher-level setup and teardown methods. `SetUpAttribute` and `TearDownAttribute` are no longer allowed. |
| TestCaseData       | The `Throws` Named Property is no longer available. Use `Assert.Throws` or `Assert.That` in your test case. |
| TestContext        | The fields available in the [[TestContext]] have changed, although the same information remains available as for NUnit V2. |

######Console Features

The console runner is now called `nunit3-console`. The following breaking changes apply to the options that  the new runner supports.

|      Option       |     Function                            |     Notes                |
|-------------------|-----------------------------------------|--------------------------|
| --fixture=STR     | Test fixture or namespace to be loaded  | No longer supported. Use --test instead. |
| --run=STR         | List of tests to run                    | No longer supported. Replaced by --test. |
| --runlist=PATH    | File containing list of tests to run    | No longer supported. Replaced by --testlist. |
| --include=LIST    | List of categories to include           | No longer supported. Use --where instead. |
| --exclude=LIST    | List of categories to exclude           | No longer supported. Use --where instead. |
| --process=PROCESS | ProcessModel for test assemblies        | Default value is now Separate for a single assembly, Multiple for more than one. Multiple assemblies run in parallel by default. |
| --domain=DOMAIN   | DomainUsage for test assemblies         | Default value is now Separate for a single assembly, Multiple for more than one. |
| --apartment=APT   | Apartment in which to run tests         | No longer supported. Use ApartmentAttribute. |
| --xmlconsole      | Display XML to the console              | No longer supported.     |
| --basepath        | Set ApplicationBase for execution       | No longer supported.     |
| --privatebinpath  | Specify probing path for execution      | No longer supported.     |
| --cleanup         | Remove left-over cache files            | No longer supported.     |
| --noshadow        | Disable shadow copy                     | No longer supported. The console runner now disables shadow copy by default. use **--shadowcopy** on the command-line to turn it on. |
| --nothread        | Disable use of a separate thread for tests  | No longer supported. |
| --nodots          | Do not display dots as a progress indicator | No longer supported. |
