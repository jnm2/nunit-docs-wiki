> **NOTE:** This page is a specification that was used as a starting point for creating the feature in NUnit. It needs to be reviewed and revised in order to accurately reflect what was actually built. If you take it with a grain of salt, it may still be helpful to you as documentation. This notice will be removed when the page is brought up to date.

The NUnit test engine is able to offer a certain degree of parallelization by running the tests in each test assembly in a different Process or ```AppDomain```. If tests are already split across multiple assemblies, this is the simplest way to improve performance through parallel execution.

This is a separate facility from [[Framework Parallel Test Execution]] although the two may be used concurrently.

####Process Model

NUnit uses the ```ProcessModel``` enumeration to specify how assemblies are split across processes. The ```ProcessModel``` for a run is specified either on the console command line, through the NUnit default settings or in the NUnit project file.

In NUnit 2.6.3, three values are defined:
  * ```ProcessModel.Single``` causes all tests to be run within the NUnit process itself.
  * ```ProcessModel.Separate``` loads and runs all the tests in a single separate process.
  * `ProcessModel.Multiple` loads and runs each test assembly in a separate process. This is done sequentially, with each process allowed to finish before the next is started.

NUnit 3.0 will define a new setting, `ProcessModel.Parallel`, creating a separate process for each test assembly and running them all in parallel.

####Domain Usage

The ```DomainUsage``` enumeration is specified in the same ways as ```ProcessModel``` and specifies how the assemblies are split across `AppDomain`s.

In NUnit 2.6.3, three values are defined:
  * `DomainUsage.None` causes NUnit to run the tests in the primary `AppDomain`. This generally requires copying some of NUnit's own assemblies to the directory containing the tests.
  * `DomainUsage.Single` runs all the tests in a separate `AppDomain`, with its own `ApplicationBase`. This is the default in most cases.
  * `DomainUsage.Multiple` runs each test assembly in a separate `AppDomain`, sequentially.

NUnit 3.0 will define a new setting, `DomainUsage.Parallel` to cause the test assemblies to be run in parallel. A separate thread will be created to run within each `AppDomain`.

####Interactions between ProcessModel and DomainUsage

The result of combining the possible values of the two enumerations ```ProcessModel``` and ```DomainUsage``` are summarized in the following table.

|                           | ```DomainUsage.None``` | ```DomainUsage.Single``` | ```DomainUsage.Multiple``` | ```DomainUsage.Parallel``` |
|----  | ---------------- | ------------------ | -------------------- | ------------------ |
| ```ProcessModel.Single``` | Tests run within NUnit's process and in the same ```AppDomain``` as NUnit itself. |Tests run within NUnit's process but in a separate ```AppDomain```. | Tests run sequentially within NUnit's process with one ```AppDomain``` for each test assembly. | Tests run within NUnit's process and each assembly runs in its own ```AppDomain```, in parallel with other assemblies. |
| ```ProcessModel.Separate``` | Tests run in the default ```AppDomain``` of a single separate process. | Tests run in a standalone ```AppDomain``` of a single separate process. | Tests run sequentially in single separate process, with one ```AppDomain``` for each assembly. | Tests run in a single separate process, with one ```AppDomain``` for each assembly which can run in parallel with other assemblies. |
| ```ProcessModel.Multiple``` | Tests run sequentially in one process per assembly, in the default ```AppDomain``` of the process. | Tests run sequentially in one process per assembly, in a standalone ```AppDomain``` within each process. | Invalid option, ```DomainUsage.Single``` will be used. | Invalid option, ```DomainUsage.Single``` will be used. |
| ```ProcessModel.Parallel``` | Tests run in one process per assembly, in the default ```AppDomain``` of the process, and each process can run tests in parallel with others. | Tests run in one process per assembly, in a standalone ```AppDomain``` within each process, and each process can run tests in parallel with others. | Invalid option, ```DomainUsage.Single``` will be used. | Invalid option, ```DomainUsage.Single``` will be used. |

Two of the process model settings, `ProcessModel.Multiple` and `ProcessModel.Parallel`, create separate processes per assembly. If you also specify `DomainUsage.Multiple` or `DomainUsage.Parallel`, the `DomainUsage` settings are ignored and the default `DomainUsage.Single` is used instead. A warning may be displayed.

We plan to eliminate support for `DomainUsage.None` except where the tests are run in a separate process form NUnit. However, the setting may still be available, but deprecated, in the 3.0 release.

####Default Settings

For now, we are keeping the default values as `ProcessModel.Single` and `DomainUsage.Single`. This may change as development proceeds.