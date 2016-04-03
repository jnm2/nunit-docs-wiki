###DRAFT
This page lists all attributes to be supported by the NUnit 3.0 framework. Not all attributes are supported equally by the various framework distributions. See [[Attribute Support|Framework-Distributions#attribute-support]] for details of where each attribute is supported.

### Existing (2.6.3) Attributes

This table lists all attributes supported by NUnit 2.6.3. Unless otherwise noted, we plan to support them without change in NUnit 3.0. Note that only user-visible changes are listed here. Many attributes have internal changes in their implementation in addition.

|  Attribute  |  Status / Notes  |
|-------------|------------------|
| CategoryAttribute             | |
| CombinatorialAttribute        | |
| CultureAttribute              | May change to function like SetCultureAttibute and take multiple values. |
| DataPointAttribute            | |
| DataPointsAttribute           | Deprecate. |
| DescriptionAttribute          | |
| ExpectedExceptionAttribute    | Remove. |
| ExplicitAttribute             | |
| IgnoreAttribute               | |
| MaxTimeAttribute              | |
| PairwiseAttribute             | |
| PlatformAttribute             | Add more platforms - see [[Platform Attribute]]. Possibly replace - see [[Include and Exclude Attributes]] |
| PropertyAttibute              | |
| RandomAttribute               | |
| RangeAttribute                | |
| RepeatAttribute               | |
| RequiredAddinAttribute        | |
| RequiresMTAAttribute          | |
| RequiresSTAAttribute          | |
| RequiresThreadAttribute       | |
| SequentialAttribute           | |
| SetCultureAttribute           | Deprecate if CultureAttribute is changed. |
| SetUICultureAttribute         | Deprecate if CultureAttribute is changed. |
| SetUpAttribute                | |
| SetUpFixtureAttribute         | Modify SetUpFixture to use OneTimeSetUp and OneTimeTearDown rather than simple SetUp and TearDown attributes. See [[SetUp and TearDown]]. |
| SuiteAttribute                | |
| TearDownAttribute             | Change in semantics. See [[SetUp and TearDown]]. |
| TestActionAttribute           | |
| TestAttribute                 | Add ExpectedResult property. |
| TestCaseAttribute             | |
| TestCaseSourceAttribute       | |
| TestFixtureAttribute          | |
| TestFixtureSetUpAttribute     | Deprecate. See [[SetUp and TearDown]]. |
| TestFixtureTearDownAttribute  | Deprecate. See [[SetUp and TearDown]]. |
| TheoryAttribute               | |
| TimeoutAttribute              | |
| ValuesAttribute               | |
| ValueSourceAttribute          | |

### New Attributes

The following new attributes are planned for the 3.0 framework.

|  Attribute  |  Status / Notes  |
|-------------|------------------|
| DataPointSourceAttribute      | Replaces DataPointsAttribute |
| LevelOfParallelismAttribute   | Determines maximum number of worker threads. See [[Framework Parallel Test Execution]]. |
| ParallelizableAttribute       | Determines which tests may be run in parallel. See [[Framework Parallel Test Execution]]. |
| OneTimeSetUpAttribute         | For use in SetUpFixture and TestFixture. See [[SetUp and TearDown]]. |
| OneTimeTearDownAttribute      | For use in SetUpFixture and TestFixture. See [[SetUp and TearDown]]. |
| IncludeAttribute              | May be defined to replace Platform and Culture. See [[Include and Exclude Attributes]] |
| ExcludeAttribute              | May be defined to replace Platform and Culture. See [[Include and Exclude Attributes]] |
