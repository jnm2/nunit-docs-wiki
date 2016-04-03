NUnit 2.6.3 was able to run tests in parallel only through use of pNUnit, which is not suitable for casual parallelization for the purpose of reducing test execution time.

NUnit 3.0 will offer three forms of parallel execution...

####Parallel Execution of Multiple Assemblies

This level of parallelism is simple to implement, provided that the tests in each assembly do not use common external resources such as files or databases. The engine is able to run the tests for each assembly in a separate process for maximum isolation. Alternatively, it can run them within the same process in separate AppDomains, creating a new thread for each domain. 

See [[Engine Parallel Test Execution]] for details.

####Parallel Execution within an Assembly

Within each assembly, the framework can run tests in parallel using a specified number of worker threads. By default, no parallel excecution takes place. Tests that are eligible to be run in parallel with other tests must be identified using the ParallelizationAttribute. Other attributes and properties are used to control how the tests are run with respect to one another.

See [[Framework Parallel Test Execution]] for details.

####Distributed Testing using PNUnit

PNUnit is designed for a different sort of parallel execution. It enables the testing of distributed applications by running cooperating tests in separate processes, potentially across multiple machines. It is not yet determined whether we will create a new version of PNUnit to work with NUnit 3.0 or if the capabilities of PNUnit will instead be built into NUnit itself.

Watch for more info on the [[PNUnit]] page.