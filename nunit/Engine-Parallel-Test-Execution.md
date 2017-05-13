The NUnit test engine is able to offer a certain degree of parallelization by running the tests in each test assembly in a different `Process`. If tests are already split across multiple assemblies, this is the simplest way to improve performance through parallel execution.

**Note:** This is a separate facility from [[Framework Parallel Test Execution]] although the two may be used concurrently.

#### Process Model

NUnit 3 uses the `ProcessModel` enumeration to specify how assemblies are split across processes. The `ProcessModel` for a run may specified either on the console command-line or in the NUnit project file.

As in NUnit V2, three values are defined:
  * `ProcessModel.Single` causes all tests to be run within the NUnit process itself.
  * `ProcessModel.Separate` loads and runs all the tests in a single separate process.
  * `ProcessModel.Multiple` loads and runs each test assembly in a separate process.

In NUnit 3, if `ProcessModel.Multiple` is used, the processes are executed in parallel. This is also the default if the `ProcessModel` is not specified.
