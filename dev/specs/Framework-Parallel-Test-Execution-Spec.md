> **NOTE:** This page is a specification that was used as a starting point for creating the feature in NUnit. It needs to be reviewed and revised in order to accurately reflect what was actually built. If you take it with a grain of salt, it may still be helpful to you as documentation. This notice will be removed when the page is brought up to date.

The NUnit 3.0 framework can run tests in parallel within an assembly. This is a completely separate facility from [[Engine Parallel Test Execution]], although it is possible to use both in the same test run.

By default, no parallel execution takes place. Attributes are used to indicate which tests may run in parallel and how they relate to other tests. The names of some attributes and properties are adapted from MbUnit, since those names are familiar to many users. However, the semantics may be slightly different in some cases.

#### ParallelizableAttribute

This attribute is used to indicate whether the test and/or its descendants may be run in parallel with other tests. The constructor takes an optional `ParallelScope` enumeration argument (see below), which defaults to `ParallelScope.Self`. The attribute may be used at the assembly, class or method level and the word "test" in the rest of this description refers to the suite or test case that corresponds to the item on which the attribute appears.

Two Named Properties are supported:
  * `Scope = ParallelScope` for setting `ParallelScope` using property syntax
  * `ExclusionGroup = string` for ensuring that certain tests do not run together (NYI)

##### ParallelScope Enumeration

This is a `[Flags]` type enumeration used to specify which tests may run in parallel. It applies to the test upon which it appears and any subordinate tests. Initially, it will use the following values:
  * `ParallelScope.None` indicates that the test may not be run in parallel with other tests.
  * `ParallelScope.Self` indicates that the test itself may be run in parallel with other tests.
  * `ParallelScope.Children` indicates that the descendants of the test may be run in parallel with respect to one another.
  * `ParallelScope.Fixtures` indicates that fixtures may be run in parallel with one another.

> Specific values may be added or removed as development proceeds.
> Values that apply to a higher level test than the test on which the scope appears - for example, ParallelScope.Fixtures appearing on a method - are ignored without warning or affect.

##### ExclusionGroup (NYI)

The string identifies a group of tests to which this one belongs. Only one test within a group may execute at the same time. Note that the exclusion only applies to the test on which the attribute appears. If the attribute indicates that descendants may run in parallel with one another, the group setting does not prevent them from doing so.

Since exclusion groups represent locks that must be acquired, we need to minimize the possiblility of deadlocks. Therefore, we only allow tests to belong to one exclusion group. However, deadlocks are still possible if child tests also specify exclusion groups. To avoid them, the following guidelines need to be followed:

  1. No child test should specify the same exclusion group as a parent.

  2. The order of specifying exclusion groups from the outermost test to the innermost should always be the same. Minimizing the number of exclusion groups used will make this easier

> We need to do some research to determine if we can avoid the problem of deadlock by simply detecting and prohibiting any violation of these guidelines.

> We may want to consider replacing the use of a string with a Type for better refactoring.

##### Specifying Parallelizable at Multiple Test Levels

The `ParallelizableAttribute` may be specified on multiple levels of the tests, with lower-level specifications overriding higher ones. Thus, if the assembly has `ParallelScope.None` either by use of the attribute or by default, classes with `ParallelScope.Self` may be run in parallel as may their children if an appropriate scope is used.

It is however important to note that a lower-level specification only applies at that level and below. It cannot override settings on higher-level tests. Thus, allowing parallel execution for methods of a class that does not allow it, results in those methods running in parallel with one another, but not in parallel with test methods under any other classes. This is the natural outcome of the fact that the execution of a test method is, in fact, part of the execution of the test represented by the class.

#### LevelOfParallelismAttribute

This is an **assembly-level** attribute, which may be used to specify the level of parallelism, that is, the maximum number of worker threads executing tests in this assembly. It may be overridden using a command-line option in the console runner. If it is not specified, NUnit uses a default value based on the number of processors available or a specified minimum, whichever is greater.

#### Parallel Execution

We use multiple queues organized into "shifts". A `WorkShift` consists of one or more queues of work items, which may be active at the same time. As the name suggests, no two shifts are active simultaneously. NUnit runs one `WorkShift` until all available work is complete and then switches to the next shift. When there is no work for any shift, the run is complete.

There are three shifts, listed here with their associated queues...

|     Shift              |    Queues              |  Workers  |  Usage    |
|------------------------|------------------------|-----------|-----------|
| Parallel Shift         | Parallel Queue         |    LoP*   | Parallelizable tests run in the MTA |
|                        | Parallel STA Queue     |     1     | Parallelizable tests run in the STA |
| Non-Parallel Shift     | Non-Parallel Queue     |     1     | Non-parallelizable tests run in the MTA |
| Non-Parallel STA Shift | Non-Parallel STA Queue |     1     | Non-parallelizable tests run in the STA |

_* Depends on Level of Parallelism_

For efficiency, each queue is created when the first test is added to it. At the time of creation, all workers for that queue are also created and initialized.

If the command line specifies zero workers, all use of the dispatcher and its queues is currently bypassed and tests are run sequentially on a single thread.

**NOTE:** In the current implementation, test methods or cases are never run in parallel with one another, even if the `ParallelizableAttribute` is specified on them.

#### Text Output from Tests

In the past, NUnit was able to capture text output (Console, Trace and Log) and associate it with the correct test. This was possible because only one test could run at a time, therefore any output received between the start and end of a particular test could be identified with that test.

In an environment where multiple tests may be running at the same time, this is no longer possible. Consequently, NUnit 3.0 will no longer capture Console, Trace or Log output. A separate facility is being added to the NUnit `TextContext` to allow writing output to the test result itself.

See [[Text Output from Tests]] for further details.

#### Platform Support

This feature is intended to be supported by the full NUnit framework on all supported platforms. It is not being supported at this time under NUnitLite. The attributes are recognized under NUnitLite but they have no effect.

#### Implementation Status

The following is done:
* All work shifts and queues described above.
* ParallelizableAttribute and LevelOfParallelismAttribute.
* NUnit-console commandline option --workers
* Fixtures may be run in parallel.

Not yet done:
* Implementation of ExclusionGroups
* Running test cases in parallel
* Special handling of text output
