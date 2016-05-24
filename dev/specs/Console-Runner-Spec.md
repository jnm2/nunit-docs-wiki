> **NOTE:** This page is a specification that was used as a starting point for creating the feature in NUnit. It needs to be reviewed and revised in order to accurately reflect what was actually built. If you take it with a grain of salt, it may still be helpful to you as documentation. This notice will be removed when the page is brought up to date.

This specification recommends implementing a command line tool for running NUnit tests.

The NUnit console runner is a text-based runner and is useful for automation of tests in build scripts and for integration into other systems, e.g. Continuous Integration server.

The features of the NUnit framework should be usable from the console runner. If possible the command line arguments should be backward compatible to the console runner of NUnit 2.5.

### User Stories

##### An NUnit User...

  * Runs all the tests from an assembly
  * Runs tests from multiple assemblies
  * Runs tests from an NUnit Project
  * Runs tests from a Visual Studio project or solution
  * Selects tests to be run by name
  * Selects tests to be run by category
  * Selects the .NET framework version for running tests
  * Determines where tests are run and how they are isolated
  * Sets options for how tests are run
  * Sets options for reporting test results
  * Specifies which tests to execute first

### Design

The console runner loads the tests from the assemblies and projects which have been specified at the command line. It uses the NUnit Test Engine to load and run the tests.

Command line options are used to specify filtering of the tests to be run and how they are run. These options 
generally override any options specified in nunit projects.

The test result is displayed on the console in a format similar to that used in NUnit 2.4 and 2.5 and an XML file with the test results is produced.

#### Command Line Format

The command line format for the console runner is

```
nunit-console [inputfiles] [options]
```

Input files may be of any file type that NUnit is able to load. This includes assemblies,
nunit projects, VS projects and solutions and any other project types for which an addin has been installed. Unlike NUnit 2.5, which was allowed multiple assemblies but only a single project on the command line, the 3.0 runner will support any mix of projects and assemblies.

See [[Command Line Options Spec]] for details of available options.

#### Communication with the Test Engine

The console runner does not actually load or run tests itself. This service is 
provided by the [[Test Engine Spec]]. In addition, the [[test engine Spec]] interprets
parameters passed from the console runner to filter tests and to determine
where and how they are to be run.

#### XML Output

The console runner always produces an XML file showing the results of
the test run. By default, it is named TestResult.xml as in NUnit 2.5,
but the name can be changed using command-line options.

Additional output files may be produced by applying xslt transforms
to the primary output file.

See [[XML Output Format]] for details of the output format.

#### Console Output

Console output from each run is similar to that produced by NUnit 2.5.
The summary report is actually produced from the XML output and the
user may replace the transform used to produce the output. This feature
was present in earlier versions of NUnit but was removed in NUnit 2.5.

#### Return Codes

The console runner returns 0 to the calling script if the run completed
successfully and all tests passed. If any errors or failures occured,
a positive return code gives the number of such errors or failures. If
the run is terminated by a fatal error, a negative return code results.

#### Extensibility

User extensibility will be provided through Mono.Addins.

### Implementation

#### Test Engine

Initial development of the Test Engine will be under this project. It may
be separated or moved elsewhere later but it's more convenient to develop
the console client and the engine together.
