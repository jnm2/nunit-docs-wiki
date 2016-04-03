##Background

NUnitLite originated in 2007 as a lightweight version of the NUnit framework. The code was developed from scratch with the intention of providing a test framework that would use minimal resources and run on resource-restricted platforms such as those used in embedded and mobile development.

At the same time, NUnitLite was used as the basis for experimentation with new framework features, which were later backported to the full NUnit framework. The fluent constraint-based assertion interface now used in NUnit originated in NUnitLite in this way.

Over time, NUnitLite has also been adopted by many people for use in the desktop .NET environment, because it provides a simpler way to run tests and one which does not depend upon remoting for execution.

With NUnit 3.0, both frameworks now share a common codebase.

##Unifying the Frameworks

We will eliminate feature differences between the NUnitLite framework and the full NUnit framework. Many of the differences will be re-characterized as platform differences. That is, for certain platforms certain features may not be supported. For example, since Silverlight does not support file access, our Silverlight build of the framework will not support file-related constraints and asserts.

The built-in runner currently in NUnitLite will become a separate assembly, linked to the framework. Those platforms like desktop .NET and Windows CE capable of running a console-based application will use the existing runner in separated form. Other platforms, like Silverlight, would need runners tailored for their environment. 

We will re-brand the term NUnitLite to mean a distribution of the framework and an associated lightweight runner for a particular platform. The framework assembly itself will no longer use the name NUnitlite. It's possible, but not yet decided, that we will call the lightweight runner `nunitlite.exe`.

Specifically, parallelism and file-related features will be supported in the framework on a platform-dependent basis. Classic Asserts will be included in order to support legacy applications that use them. On every platform, we would aim to implement as much of NUnit as is possible.

###Implementation

The following issues have been created in order to implement this spec:

  * [#325 Add RegexConstraint to Compact Framework build](https://github.com/nunit/nunit/issues/325)
  * [#326 Add TimeoutAttribute to compact framework build](https://github.com/nunit/nunit/issues/326)
  * [#327 Allow Generic test methods in the compact framework](https://github.com/nunit/nunit/issues/327)
  * [#328 Use .NET Stopwatch class for compact framework builds](https://github.com/nunit/nunit/issues/328)
  * [#333 Add parallel execution to desktop builds of NUnitLite](https://github.com/nunit/nunit/issues/333)
  * [#334 Include File-related constraints and syntax in NUnitLite builds](https://github.com/nunit/nunit/issues/334)
  * [#335 Re-introduce 'Classic' NUnit syntax in NUnitLite](https://github.com/nunit/nunit/issues/335)
  * [#341 Move the NUnitLite runners to separate assemblies](https://github.com/nunit/nunit/issues/341)

##Detailed Discussion

The sections that follow capture some of the details of the discussion that led up to the decision to unify NUnit and NUnitLite.

### Added Features

####Platform Support

NUnitLite runs under Silverlight and the Compact framework, in addition to the desktop .NET and mono platforms.

#####Actions:
  * Continue to support desktop and Silverlight platforms
  * Drop support for version 2.0 of the Compact Framework
  * Add support for version 3.9 of the Compact Framework
  * Develop a portable build and subsequently evaluate whether it can be used to replace any existing builds

####Built-In Runner

NUnitLite has a built-in runner, allowing it to be used without the NUnit Test Engine or any external runner. This is the primary justification for calling it "lite" at the present time.

#####Actions:
  * Remove the current NUnitLite text-based runner from the framework assembly and create it as a separate assembly, linked to the framework. We can use this runner for desktop .NET and CF.
  * Create a separated runner for Silverlight and the portable builds.

### Missing Features

####Parallelism

The full NUnit framework supports parallel execution of tests. NUnitLite does not but rather executes all tests sequentially on a single thread. The ParallelizableAttribute is accepted but ignored by NUnitLite and a number of internal classes that support parallel execution are not present.

The full NUnit framework contains code to execute tests sequentially, like NUnitLite. This execution path is activated when running under the console with /workers=0. The sequential path is also used by TestSuites to execute individual cases on the same thread.

#####Actions:
  * Add support for parallel execution to NUnitLite on a platform-by-platform basis. Desktop platforms and CF 3.9 should be able to support it. **Issue #333 created**
  * Reduce use of the sequential execution path as much as possible in both NUnit and NUnitLite, replacing it by a dispatcher that uses a single worker. This internal change will reduce special cases in the code but should not be visible to users.

####File-Related Features

NUnitLite does not include the constraints and asserts that apply to files.

#####Actions:
  * Add support for constraints and asserts on a platform-by-platform basis rather than excluding them for all NUnitLite builds. Most features will then be supported on the desktop and in CF but not in Silverlight. **Issue #334 Created**

####Classic Asserts

When NUnitLite was written, we planned to phase out "classic" asserts in favor of the user of Assert.That with constraints. Therefore, NUnitLite does not include classic Asserts, with the exception of True, False, Null, NotNull, AreEqual and AreNotEqual. 

As things have turned out, resistance to elimination of the classic Asserts has been strong. They continue to exist in NUnit, where they have not even been deprecated.

Specifically the following methods of Assert are present in NUnit but excluded from NUnitLite:
  * IsNaN
  * IsEmpty
  * IsNotEmpty
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

In addition, the following extended assert classes are absent in NUnitLite:
  * StringAssert
  * CollectionAssert
  * FileAssert
  * DirectoryAssert

#####Actions
  * These features should be added to NUnitLite  for platforms that support them. **Issue #335 Created**

##Platform-Specific Differences

A number of features that are not generally omitted from NUnitLite are missing on specific platforms.

####BinarySerializableConstraint

This constraint and associated syntax are not implemented on either the compact framework or Silverlight because the platforms don't support binary serialization.

#####Actions:
  * None

####XmlSerializableConstraint

This constraint and associated syntax is not implemented on Silverlight.

#####Actions:
  * None.

####RegexConstraint

This constraint and associated syntax are not implemented in our compact framework builds because it was not supported in earlier versions.

#####Actions:
  * Implement in CF 3.5 and higher. **Issue #325 Created**

####SetCultureAttribute and SetUICultureAttribute

These attributes are not implemented on the compact framework.

#####Actions:
  * None

####TimeoutAttribute

This attribute is not implemented in our compact framework builds, because it was not possible to support in earlier versions.

#####Actions:
  * Implement in CF 3.5 and higher. **Issue #326 Created**

####Generic Test Methods

This is not available in our CF builds, due to differences in the internal implementation of generics in CF.

#####Actions:
  * Incorporate Neil's code that implements generic test methods. **Issue #327 Created**

####Use of Stopwatch for Timing Tests

Our compact framework and Silverlight builds use a private version of Stopwatch based on the time of day, which gives us a much lower resolution. In the case of CF, this is because earlier versions of the framework didn't have Stopwatch.

#####Actions:
  * Use .NET Stopwatch in the CF builds. **Issue #328 Created**

