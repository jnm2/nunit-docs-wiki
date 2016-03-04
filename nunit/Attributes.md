NUnit uses custom atributes to identify tests. All NUnit attributes are contained in the NUnit.Framework namespace. Each source file that contains tests must include a using statement for that namespace and the project must reference the framework assembly, `nunit.framework.dll`.

This table lists all the attributes supported by NUnit. 

|   Attribute                       |    Usage    |
|-----------------------------------|-------------|
| [[Apartment Attribute]]           | Indicates that the test should run in a particular apartment. |
| [[Author Attribute]]              | Provides the name of the test author. |
| [[Category Attribute]]            | Specifies one or more categories for the test. |
| [[Combinatorial Attribute]]       ||
| [[Culture Attribute]]             ||
| [[Datapoint Attribute]]           ||
| [[DatapointSource Attribute]]     ||
| [[Description Attribute]]         ||
| [[Explicit Attribute]]            ||
| [[Ignore Attribute]]              ||
| [[LevelOfParallelism Attribute]]  ||
| [[Maxtime Attribute]]             ||
| [[OneTimeSetUp Attribute]]        ||
| [[OneTimeTearDown Attribute]]     ||
| [[OrderAttribute]]                ||
| [[Pairwise Attribute]]            ||
| [[Parallelizable Attribute]]      ||
| [[Platform Attribute]]            ||
| [[Property Attribute]]            ||
| [[Random Attribute]]              ||
| [[Range Attribute]]               ||
| [[Repeat Attribute]]              ||
| [[RequiresThread Attribute]]      ||
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
