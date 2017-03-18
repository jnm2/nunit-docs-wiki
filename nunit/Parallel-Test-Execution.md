NUnit 3.0 offers two forms of parallel execution, allowing tests to be run more quickly.

## Parallel Execution of Multiple Assemblies

The NUnit test engine is able to offer a certain degree of parallelization by running the tests in each test assembly in a different Process. If tests are already split across multiple assemblies, this is the simplest way to improve performance through parallel execution.

In order to use this level of parallelism is simple to implement, that the tests in each assembly must not use any common external resources such as files or databases. **This is the default behavior when running multiple assemblies together.**

Normally, all the test processes run simultaneously. If you need to reduce the number of processes allowed to run at one time, you may specify a value for the `--agents` option on the nunit-console command-line. For example, if you are running tests in 10 different processes, a setting of `--agents=3` will allow no more than three of them to execute simultaneously.

**Note:** This facility does not depend on the test framework used in any way. Test assemblies that use older versions of NUnit may be run in parallel processes just as easily as those using NUnit 3.0. If extensions are created to support additional frameworks, the NUnit engine will run those assemblies in parallel as well.

## Parallel Execution within an Assembly

The NUnit 3.0 framework can run tests in parallel within an assembly. By default, no parallel excecution takes place. Tests that are eligible to be run in parallel with other tests must be identified using the [[Parallelizable Attribute]].

The framework creates worker threads for running tests. The default number of threads is equal to the number of processors or 2, whichever is greater. The user can control the number of threads by use of the assembly-level [[LevelOfParallelism Attribute]] or the `--workers` option on the command-line. The command-line option takes precedence, if specified.

Parallel execution in the framework requires some attention to how tests are written. Use of non-readonly statics or access to common internal or external resources can easily break your tests or hang the test run. Race conditions may result in problems that arise only intermittently and are very difficult to resolve. Once we implement parallel execution of test cases, shared use of instance members will be dangerous as well. Tests to be run in parallel should generally be stateless.

#### How It Works

We use multiple queues organized into "shifts". A `WorkShift` consists of one or more queues of work items, which may be active at the same time. As the name suggests, no two shifts are active simultaneously. NUnit runs one `WorkShift` until all available work is complete and then switches to the next shift. When there is no work for any shift, the run is complete.

There are three shifts, listed here with their associated queues...

|     Shift              |    Queues              |  Workers  |  Usage    |
|------------------------|------------------------|-----------|-----------|
| Parallel Shift         | Parallel Queue         |    LoP*   | Parallelizable tests run in the MTA |
|                        | Parallel STA Queue     |     1     | Parallelizable tests run in the STA |
| Non-Parallel Shift     | Non-Parallel Queue     |     1     | Non-parallelizable tests run in the MTA |
| Non-Parallel STA Shift | Non-Parallel STA Queue |     1     | Non-parallelizable tests run in the STA |

_* Depends on Level of Parallelism_

**NOTES:**

1. As can be seen in the table, if `--workers=n` is specified, n + 3 workers are actually created and up to n + 1 workers may be active at one time. This extra worker has little impact on throughput, since tasks in the STA tend to spend a good deal of time waiting.

2. For efficiency, each queue is created when the first test is added to it. At the time of creation, all workers for that queue are also created and initialized.

3. If the command line specifies zero workers, all use of the dispatcher and its queues is currently bypassed and tests are run sequentially on a single thread.

4. In the current implementation, test methods or cases are never run in parallel with one another, even if the `ParallelizableAttribute` is specified on them.

#### Text Output from Tests

In the past, NUnit was able to capture text output (Console, Trace and Log) and associate it with the correct test. This was possible because only one test could run at a time, therefore any output received between the start and end of a particular test could be identified with that test.

In an environment where multiple tests may be running at the same time, this is no longer possible. To solve this problem, output is now collected in the result for each test and is not displayed until the test completes.

#### Platform Support

This feature is supported by .NET 2.0, 4.0, 4.5 and Compact Framework builds of the NUnit framework. It is not available in the  Silverlight or Portable builds. Where not supported, the related attributes are still accepted but are ignored.
