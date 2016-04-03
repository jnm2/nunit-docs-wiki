NUnit uses custom attributes to identify tests. All NUnit attributes are contained in the NUnit.Framework namespace. Each source file that contains tests must include a using statement for that namespace and the project must reference the framework assembly, `nunit.framework.dll`.

This table lists all the attributes supported by NUnit. 

|   Attribute                       |    Usage    |
|-----------------------------------|-------------|
| [[Apartment Attribute]]           | Indicates that the test should run in a particular apartment. |
| [[Author Attribute]]              | Provides the name of the test author. |
| [[Category Attribute]]            | Specifies one or more categories for the test. |
| [[Combinatorial Attribute]]       | Generates test cases for all combinations of individual data items provided. |
| [[Culture Attribute]]             | Specifies cultures for which a test or fixture should be run. |
| [[Datapoint Attribute]]           | Provides data for Theories. [obsolete?] |
| [[DatapointSource Attribute]]     | Provides data for Theories. |
| [[Description Attribute]]         | Applies descriptive text to a Test, TestFixture or Assembly. |
| [[Explicit Attribute]]            | Flags decorated test to be skipped unless explicitly run. |
| [[Ignore Attribute]]              | Indicates that a test shouldn't be run for some reason. |
| [[LevelOfParallelism Attribute]]  | Specifies the level of parallelism at assembly level. |
| [[Maxtime Attribute]]             | Specifies the maximum time in milliseconds for a test case. |
| [[OneTimeSetUp Attribute]]        | Identifies methods to be called once prior to any test in fixture. |
| [[OneTimeTearDown Attribute]]     | Identifies methods to be called once after all tests in fixture. |
| [[Order Attribute]]               | Specifies the order in which decorated test should be run (against others). |
| [[Pairwise Attribute]]            ||
| [[Parallelizable Attribute]]      | Indicates whether test and/or its descendants can be run in parallel. |
| [[Platform Attribute]]            | Specifies platforms for which a test or fixture should be run. |
| [[Property Attribute]]            ||
| [[Random Attribute]]              ||
| [[Range Attribute]]               ||
| [[Repeat Attribute]]              | Specifies that the decorated method should be executed multiple times. |
| [[RequiresThread Attribute]]      | Indicates that a test method, class or assembly should be run on a separate thread. |
| [[Retry Attribute]]               ||
| [[Sequential Attribute]]          ||
| [[SetCulture Attribute]]          ||
| [[SetUICulture Attribute]]        ||
| [[Setup Attribute]]               ||
| [[SetupFixture Attribute]]        ||
| [[Teardown Attribute]]            ||
| [[Test Attribute]]                ||
| [[TestCase Attribute]]            ||
| [[TestCaseSource Attribute]]      ||
| [[TestFixture Attribute]]         ||
| [[TestFixtureSetup Attribute]]    ||
| [[TestFixtureSource Attribute]]   ||
| [[TestFixtureTeardown Attribute]] ||
| [[TestOf Attribute]]              ||
| [[Theory Attribute]]              ||
| [[Timeout Attribute]]             ||
| [[Values Attribute]]              ||
| [[ValueSource Attribute]]         ||