> **NOTE:** This page is a specification that was used as a starting point for creating the feature in NUnit. It needs to be reviewed and revised in order to accurately reflect what was actually built. If you take it with a grain of salt, it may still be helpful to you as documentation. This notice will be removed when the page is brought up to date.

This spec describes features present in various distributions of the NUnit framework. 

Currently, there are two main framework distributions, each of which may be built
for multiple platforms:

  * The full NUnit framework, referred to hereafter as 'NUnit'
  * The NUnitLite framework, referred to as 'NUnitLite' 

### Runtime Platforms Supported

##### NUnit

  * .Net 2.0, 3.5, 4.0, 4.5
  * Mono 2.0, 3.5, 4.0, 4.5 profiles

##### NUnitLite

  * .NET 2.0, 3.5, 4.0, 4.5
  * Mono 2.0, 3.5, 4.0, 4.5 profiles
  * Silverlight 5.0
  * .NET CF 3.5

<note>NUnit and NUnitLite 3.0 no longer support the .NET 1.0 and 1.1 platforms, the Mono 1.0 profile or .NET CF 1.0 and 2.0.</note>

### Assembly Names

Builds of the framework for different runtimes are kept in separate directories and are
not distinguished by name. The following assemblies are distributed:

|  Name  |  Description  |
|--------|---------------|
| nunit.framework.dll        | The NUnit framework assembly                |
| nunit.framework.tests.dll  | Tests of the NUnit framework                |
| nunit.testdata.dll         | Data used by the NUnit tests                |
| nunitlite.dll              | The NUnitLite framework assembly            |
| nunitlite.tests.dll        | Tests of the NUnitLite framework            |
| nunitlite.testdata.dll     | Data used by the NUnitLite tests            |

### Differences in Feature Sets

Note that these lists reflect current syntax, which could change as we proceed.
Feature support for any additional platforms is not yet determined
and will be added here at a later time.

#### NUnitLite

  * NUnitLite has a built-in runner, allowing it to be used without the NUnit Test Engine or any external runner.

  * "Classic" Asserts are not supported, with the exception of True, False, Null, NotNull, AreEqual and AreNotEqual. Consequently, the following methods of Assert are not present in NUnitLite:
    * IsNaN
    * IsEmpty
    * IsNotEmpty
    * IsNullOrEmpty
    * IsNotNullOrEmpty
    * IsAssignableFrom
    * IsNotAssignableFrom
    * IsAssignableTo
    * IsNotAssignableTo
    * IsInstanceOf
    * IsNotInstanceOf
    * Greater
    * Less
    * GreaterOrEqual
    * LessOrEqual
    * Contains

  * The following extended assert classes are absent in NUnitLite:
    * StringAssert
    * CollectionAssert
    * FileAssert
    * DirectoryAssert

##### To Be Determined

The following features are currently not implemented in NUnitLite, but will be considered for addition as development progresses:

  * Attributes
    * RepeatAttribute
    * RequiresMTAAttribute
    * RequiresSTAAttribute
    * RequiresThreadAttribute
    * SuiteAttribute

##### Compact Framework Build of NUnitLite

In addition to those listed above, the following features are not available in the .NET CF builds of NUnitLite:

  * Constraints
    * BinarySerializableConstraint
    * DelayedConstraint
    * RegexConstraint

  * Attributes
    * SetCultureAttribute
    * SetUICultureAttribute
    * TimeoutAttribute

##### Silverlight Build of NUnitLite

In addtion to the general list, the following are not available in the Silverlight builds of NUnitLite:

  *Constraints
    * BinarySerializableConstraint

#### .NET 3.5 Builds

The following additional features are available in the .NET 3.5 Builds

  * Support for Extension Methods
  * Support for Lambdas

It's not yet determined whether these features will be supported under the compact framework.

#### .NET 4.0 Builds

Additional features for the .NET 4.0 builds have not yet been defined.

### Unresolved Issues

  * Decide on naming convention for NUnitLite .NET CF builds
  * Decide on version support for .NET Micro Framework - should this be an 'UltraLite'  build?
  * Decide on packageing for Silverlight and Moonlight and whether it will be based on full NUnit or NUnitLite
