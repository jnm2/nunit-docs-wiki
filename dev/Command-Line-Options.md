The command line format for the console runner is

```
nunit-console [inputfiles] [options]
```

By default, nunit-console runs the tests contained in the assemblies and projects given on the command line. If the /explore option is used, no tests are executed but a description of the tests is output.

#### Input Files

An input file may be a managed assembly (.dll or .exe) containing tests or a project file recognized by NUnit. Out of the box, the following project types are recognized:
  * NUnit project files (.nunit)
  * Visual Studio solutions (.sln)
  * Visual Studio projects (.csproj, .vbproj, .csproj) [VERIFY]
Additional project types may be available if supported by an installed addin.

Unlike NUnit 2.x, NUnit 3.0 allows multiple project files on the command line, possibly mixed with assemblies. All tests are run and combined reports and output files are produced.

#### Options

Options may be specified in any order and may be intermixed with input files. Under Windows, options are delimited by the / or - character. Under Linux, only the - is supported, since / represents the start of an absolute path.

Some project file formats, in particular the .nunit format, allow specifying certain options within the file. When a conflicting command-line option is used, it overrides the option specified in the project file.

In the tables below, NUnit 2.6.3 is used as a reference point for comparison.

##### NUnit 3.0 Options

| Option           | Function                                            | Comments and Cnanges  |
|------------------|-----------------------------------------------------|-----------------------|
| -test=NAMES      | Comma-separated list of names of the test cases, fixtures or namespaces to run or explore. Regular expressions are allowed. This option may be repeated.  | New - replaces /run   |
| -runfirst=NAME   | Name of the test case, fixture or namespace to run before the other tests. This option may be repeated. | New - NYI |
| -include=NAMES   | List of categories to include                       | Same as 2.6.3         |
| -exclude=NAMES   | List of categories to exclude                       | Same as 2.6.3         |
| -config=NAME     | Project configuration (e.g.: Debug) to load.        | Same as 2.6.3         |
| -process=ENUM    | Process model for tests: Single, Separate, Multiple | Default is now Separate for a single file and Multiple for more than one files  |
| -domain=ENUM     | AppDomain usage for tests: None, Single, Multiple   | Same as 2.6.3         |
| -framework=STR   | Framework to use for tests                          | Same as 2.6.3         |
| -x86             | Run in 32-bit process on a 64-bit system            | New option            |
| -dispose-runners | Dispose each runner after the run has ended         | New option            |
| -timeout=INT     | Timeout for each test case in milliseconds.         | Same as 2.6.3         |
| -seed=INT        | Sets random Seed used to generate cases             | New option            |
| -workers=INT     | Sets number of worker threads to use for  tests     | New option            |
| -stoponerror     | Stop run immediately after any failure or error     | Same as 2.6.3         |
| -wait            | Wait for input before closing the console window    | Same as 2.6.3         |
| -pause           | Pause before run to allow debugging                 | New option            |
| -work=PATH       | Path of the directory to use for output files.      | Same as 2.6.3         |
| -output=PATH     | File to receive test output                         | Same as 2.6.3         |
| -err=PATH        | File to receive test error output                   | Same as 2.6.3         |
| -result=SPEC     | Output SPEC for saving the test results. This option may be repeated to produce multiple output files. | See 'Output Specification Format' below. |
| -explore[=SPEC]  | Display or save test info rather than running tests. If no output specification is provided, a list of test cases is written to the console. This option may be repeated to produce multiple output files. | See 'Output Specification Format' below. |
| -noresult        | Don't save any results                              | Same as 2.6.3         |
| -labels=ENUM     | Specify whether to write test case names to the output. Values: Off, On, All. On is the default. | Was a simple boolean option in 2.6.3 |
| -trace=ENUM      | Set internal trace level: Off, Error, Warning, Info, Verbose (Debug) | Same as 2.6.3 |
| -teamcity        | Turns on use of TeamCity service messages           | New option            |
| -noheader, -noh  | Suppress display of the header info                 | Replaces /nologo      |
| -nocolor, -noc   | Display console output without color                | New option            |
| -verbose, -v     | Display additional info as the test runs            | New option            |
| -help            | Display help                                        | Same as 2.6.3         |

##### No Longer Supported

| Option          | Function                                            | Comments              |
|-----------------|-----------------------------------------------------|-----------------------|
| -fixture=STR    | Test fixture or namespace to be loaded              | Use /test instead     |
| -run=STR        | List of tests to run.                               | Replaced by /test     |
| -runlist=PATH   | File containing list of tests to run                | Replaced by /testlist |
| -apartment=APT  | Specify apartment in which to run tests             | Use ApartmentAttribute|
| -xmlConsole     | Display XML to the console                          ||
| -basepath       | Set ApplicationBase for execution                   ||
| -privatebinpath | Specify probing path for execution                  ||
| -cleanup        | Remove left-over cache files                        ||
| -noshadow       | Disable shadow copy                                 ||
| -nothread       | Disable use of a separate thread for tests          ||
| -nodots         | Do not display dots as a progress indicator         ||

##### Output Specification Format

An output specification may take one of the following forms:

  * --OPTION:filename
  * --OPTION:format=formatname
  * --OPTION:transform=xsltfile

Formats are initially all built-in, although extension through addins may be supported in the future. 

The allowed formats for the /result option are:
  * nunit3 - the native XML format for NUnit 3.0
  * nunit2 - legacy XML format used by earlier releases of NUnit
  * user   - user XSL transform. A format must be  specified. 
If no -result option is specified, output goes to TestResult.xml in the work directory.

The allowed formats for the /explore option are:
  * nunit3 - the native XML format for NUnit 3.0
  * user   - user XSL transform. A format must be specified.
  * cases  - a text file listing the full names of all test cases

If a transform is provided, user format is assumed. Otherwise, the default format is 'nunit3' for file output and 'cases' when /explore is used without a filename.
