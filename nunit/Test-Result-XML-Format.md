##&lt;test-run&gt;
The required root element for any NUnit 3.0 test result file.
 * **Containing Elements:** None
 * **Contained Elements:** [&lt;environment&gt;](#environment), [&lt;command-line&gt;](#command-line), [&lt;settings&gt;](#settings), [&lt;filter&gt;](#filter), [&lt;test-suite&gt;](#test-suite)
 * **Attributes:**
    * **id** The unique ID of this test. For the test-run, it is hard-coded as "2".
    * **testcasecount** The number of test cases contained in this test run.
    * **result** The basic result of the test. May be Passed, Failed, Inconclusive or Skipped.
    * **total** The total number of test cases executed in the run. This may be less than the testcasecont due to filtering of tests.
    * **passed** The number of test cases that passed.
    * **failed** The number of test cases that failed.
    * **inconclusive** The number of test cases that were inconclusive.
    * **skipped** The number of test cases that were skipped.
    * **asserts** The number of asserts executed in the test run.
    * **start-time** The UTC time that the test run started.
    * **end-time** The UTC time that the test run ended.
    * **duration** The duration of the test run in seconds, expressed as a real number.

##&lt;environment&gt;
Describes the environment in which the test is being run. 
> **Issue:** Some of the attributes should probably be on the assembly-level test-suite element.

 * **Containing Elements:** [&lt;test-run&gt;](#test-run)
 * **Contained Elements:** None
 * **Attributes:**
    * **nunit-version** The version of the NUnit test engine in use.
    * **clr-version** The runtime version, taken from Environment.Version.
    * **os-version** A text string describing the operating system, taken from Environment.OsVersion.
    * **platform** The platform id, taken from Environment.OsVersion.Platform.
    * **cwd** The current working directory path, taken from Environment.CurrentDirectory.
    * **machine-name** The machine name, taken from Environment.MachineName.
    * **user** The user id, taken from Environment.UserName.
    * **user-domain** The user domain, taken from Environment.UserDomainName.
    * **culture** The current culture, taken from CultureInfo.CurrentCulture.
    * **uiculture** The current UI culture, taken from CultureInfo.CurrentUICulture.
    * **os-architecture** The architecture, taken from GetProcessorArchitecture().

##&lt;command-line&gt;
Holds a CDATA section containing the text of the command used to run the tests.
 * **Containing Elements:** [&lt;test-run&gt;](#test-run)
 * **Contained Elements:** None
 * **Attributes:** None

##&lt;settings&gt;
Settings used by the engine for this run. These are taken from the supplied settings in the `TestPackage` supplemented by default settings created by the engine itself.
> **Issue:** Some settings don't appear at the top level, but only on subpackages. Should we include these settings on the assembly-level test-suite element?

 * **Containing Elements:** [&lt;test-run&gt;](#test-run)
 * **Contained Elements:** [&lt;setting&gt;](#setting)
 * **Attributes:** None

##&lt;filter&gt;
The XML representation of the filter used to execute tests.  This element is also used as a fragment in passing the filter to a runner and by the NUnit 3.0 framework and driver.

 * **Containing Elements:** [&lt;test-run&gt;](#test-run)
 * **Contained Elements:** [&lt;or&gt;](#or), [&lt;and&gt;](#and), [&lt;not&gt;](#not), [&lt;id&gt;](#id), [&lt;test&gt;](#test), [&lt;class&gt;](#class), [&lt;method&gt;](#method), [&lt;cat&gt;](#cat)
 * **Attributes:** None

##&lt;or&gt;
Represents a composite filter that contains other filters. At least one of the contained filters must pass in order for this filter to pass.

 * **Containing Elements:** [&lt;filter&gt;](#filter), [&lt;or&gt;](#or), [&lt;and&gt;](#and), [&lt;not&gt;](#not)
 * **Contained Elements:** [&lt;or&gt;](#or), [&lt;and&gt;](#and), [&lt;not&gt;](#not), [&lt;id&gt;](#id), [&lt;test&gt;](#test), [&lt;class&gt;](#class), [&lt;method&gt;](#method), [&lt;cat&gt;](#cat), [&lt;prop&gt;](#prop)
 * **Attributes:** None

##&lt;and&gt;
Represents a composite filter that contains other filters. All of the contained filters must pass in order for this filter to pass.

 * **Containing Elements:** [&lt;filter&gt;](#filter), [&lt;or&gt;](#or), [&lt;and&gt;](#and), [&lt;not&gt;](#not)
 * **Contained Elements:** [&lt;or&gt;](#or), [&lt;and&gt;](#and), [&lt;not&gt;](#not), [&lt;id&gt;](#id), [&lt;test&gt;](#test), [&lt;class&gt;](#class), [&lt;method&gt;](#method), [&lt;cat&gt;](#cat), [&lt;prop&gt;](#prop)
 * **Attributes:** None

##&lt;not&gt;
Represents a composite filter that contains wraps a single base filters. The base filter must fail in order for this filter to pass.

 * **Containing Elements:** [&lt;filter&gt;](#filter), [&lt;or&gt;](#or), [&lt;and&gt;](#and), [&lt;not&gt;](#not)
 * **Contained Elements:** [&lt;or&gt;](#or), [&lt;and&gt;](#and), [&lt;not&gt;](#not), [&lt;id&gt;](#id), [&lt;test&gt;](#test), [&lt;class&gt;](#class), [&lt;method&gt;](#method), [&lt;cat&gt;](#cat), [&lt;prop&gt;](#prop)
 * **Attributes:** None

##&lt;id&gt;
Represents a filter that examines the test id, which is generated by NUnit.

 * **Containing Elements:** [&lt;filter&gt;](#filter), [&lt;or&gt;](#or), [&lt;and&gt;](#and), [&lt;not&gt;](#not)
 * **Contained Elements:** None
 * **Attributes:** None

##&lt;test&gt;
 * **Containing Elements:** [&lt;filter&gt;](#filter), [&lt;or&gt;](#or), [&lt;and&gt;](#and), [&lt;not&gt;](#not)
 * **Contained Elements:** None
 * **Attributes:**
    * **re** Set to '1' to indicate that a regular expression comparison is to be used.

##&lt;class&gt;
 * **Containing Elements:** [&lt;filter&gt;](#filter), [&lt;or&gt;](#or), [&lt;and&gt;](#and), [&lt;not&gt;](#not)
 * **Contained Elements:** None
 * **Attributes:**
    * **re** Set to '1' to indicate that a regular expression comparison is to be used.

##&lt;method&gt;
 * **Containing Elements:** [&lt;filter&gt;](#filter), [&lt;or&gt;](#or), [&lt;and&gt;](#and), [&lt;not&gt;](#not)
 * **Contained Elements:** None
 * **Attributes:**
    * **re** Set to '1' to indicate that a regular expression comparison is to be used.

##&lt;prop&gt;
 * **Containing Elements:** [&lt;filter&gt;](#filter), [&lt;or&gt;](#or), [&lt;and&gt;](#and), [&lt;not&gt;](#not)
 * **Contained Elements:** None
 * **Attributes:**
    * **name** The name of the property to filter on.
    * **re** Set to '1' to indicate that a regular expression comparison is to be used.

##&lt;cat&gt;
 * **Containing Elements:** [&lt;filter&gt;](#filter), [&lt;or&gt;](#or), [&lt;and&gt;](#and), [&lt;not&gt;](#not)
 * **Contained Elements:** None
 * **Attributes:** None

##&lt;setting&gt;
A single setting
 * **Containing Elements:** [&lt;settings&gt;](#settings)
 * **Contained Elements:** None
 * **Attributes:**
    * **name** The name of the setting.
    * **value** The value assigned to the setting.

##&lt;test-suite&gt;
 * **Containing Elements:** [&lt;test-run&gt;](#test-run), [&lt;test-suite&gt;](#test-suite)
 * **Contained Elements:** [&lt;properties&gt;](#properties), [&lt;reason&gt;](#reason), [&lt;failure&gt;](#failure), [&lt;output&gt;](#output), [&lt;test-suite&gt;](#test-suite), [&lt;test-case&gt;](#test-case)
 * **Attributes**
    * **type** The type of suite represented by this element. Currently supported types are Assembly, TestSuite, TestFixture, 
    * **id** The unique id of this test. Coded as "mmm-nnn" where the part before the hyphen represents the assembly and the part after it represents a test in that assembly. Currently, mmm and nnn are ints, but that is merely an accident of the implementation and should not be relied on.
    * **name** The display name of the test as generated by NUnit.
    * **fullname** The full name of the test as generated by NUnit.
    * **classname** The full name of the class (fixture) representing this test. Only present if `type` is equal to "TestFixture".
    * **testcasecount** The number of test cases contained, directly or indirectly, in this suite.
    * **runstate** An indicator of whether the suite is runnable. Value may be NotRunnable, Runnable, Explicit, Skipped or Ignored. NotRunnable means there is an error in how the test is expressed in code, for example, the signature may be wrong. Explicit, Skipped and Ignored are set by attributes on the test.
    * **result** The basic result of the test. May be Passed, Failed, Inconclusive or Skipped.
    * **label** Additional labeling information about the result. In principle, this may be any string value and is combined with the result to give a more precise reason for failure. Currently, NUnit may use the following labels in combination with the Failure result: Error, Cancelled or Invalid. It may use the following labels in combination with a Skipped result: Ignored or Explicit. Additional values may be added in future releases or supplied by extensions, so code that processes a result file should be prepared to deal with any label or none at all.
    * **site** Optional element indicating where a failure occured. Values are Test, SetUp, TearDown, Parent or Child. Default is Test and the attribute does not normally appear in that case.
    * **start-time** The UTC time that the suite started.
    * **end-time** The UTC time that the suite ended.
    * **duration** The duration of the suite in seconds, expressed as a real number.
    * **total** The total number of test cases executed under this suite.
    * **passed** The number of test cases that passed.
    * **failed** The number of test cases that failed.
    * **inconclusive** The number of test cases that were inconclusive.
    * **skipped** The number of test cases that were skipped.
    * **asserts** The number of asserts executed by the suite, including any nested suites or test cases. Since asserts may be executed in OneTimeSetUp and in ActionAttributes, this number can be greater than the total of the asserts for the test cases.

##&lt;test-case&gt;
 * **Containing Elements:** [&lt;test-suite&gt;](#test-suite)
 * **Contained Elements:** [&lt;properties&gt;](#properties), [&lt;reason&gt;](#reason), [&lt;failure&gt;](#failure), [&lt;output&gt;](#output)
 * **Attributes**
    * **id** The unique id of this test. Coded as "mmm-nnn" where the part before the hyphen represents the assembly and the part after it represents a test in that assembly. Currently, mmm and nnn are ints, but that is merely an accident of the implementation and should not be relied on.
    * **name** The display name of the test as generated by NUnit or, in the case of some parameterized tests, specified by the user.
    * **fullname** The full name of the test as generated by NUnit.
    * **methodname** The name of the method representing the test case.
    * **classname** The full name of the class in which this test case appears.
    * **runstate** An indicator of whether the suite is runnable. Value may be NotRunnable, Runnable, Explicit, Skipped or Ignored. NotRunnable means there is an error in how the test is expressed in code, for example, the signature may be wrong. Explicit, Skipped and Ignored are set by attributes on the test.
    * **seed** The seed used to generate random arguments and other values for this test.
    * **result** The basic result of the test. May be Passed, Failed, Inconclusive or Skipped.
    * **label** Additional labeling information about the result. In principle, this may be any string value and is combined with the result to give a more precise reason for failure. Currently, NUnit may use the following labels in combination with the Failure result: Error, Cancelled or Invalid. It may use the following labels in combination with a Skipped result: Ignored or Explicit. Additional values may be added in future releases or supplied by extensions, so code that processes a result file should be prepared to deal with any label or none at all.
    * **site** Optional element indicating where a failure occured. Values are Test, SetUp, TearDown, Parent or Child. Default is Test and the attribute does not normally appear in that case.
    * **start-time** The UTC time that the test started.
    * **end-time** The UTC time that the test ended.
    * **duration** The duration of the test in seconds, expressed as a real number.
    * **asserts** The number of asserts executed by the test.

##&lt;properties&gt;
Optional element containing any properties assigned to the test case or suite.
 * **Containing Elements:** [&lt;test-suite&gt;](#test-suite), [&lt;test-case&gt;](#test-case)
 * **Contained Elements:** [&lt;property&gt;](#property)
 * **Attributes** None

##&lt;property&gt;
A single property
 * **Containing Elements:** [&lt;properties&gt;](#properties)
 * **Contained Elements:** None
 * **Attributes**
    * **name** The name of the property
    * **value** The value of the property

##&lt;reason&gt;
Optional element that may appear on tests or suites that were not executed. Contains a message giving the reason for skipping the test.
 * **Containing Elements:** [&lt;test-suite&gt;](#test-suite), [&lt;test-case&gt;](#test-case)
 * **Contained Elements:** [&lt;message&gt;](#message)
 * **Attributes** None

##&lt;failure&gt;
Optional element that appears on all tests or suites with a result of 'Failed'. Contains the error message and optionally a stack trace.
 * **Containing Elements:** [&lt;test-suite&gt;](#test-suite), [&lt;test-case&gt;](#test-case)
 * **Contained Elements:** [&lt;message&gt;](#message), [&lt;stack-trace&gt;](#stack-trace)
 * **Attributes** None

##&lt;message&gt;
Optional element with a CDATA section containing a message relating to the test's result.
* **Containing ELements:** [&lt;failure&gt;](#failure), [&lt;reason&gt;](#reason)
* **Contained Elements:** None
* **Attributes: None

##&lt;stack-trace&gt;
Optional element with a CDATA section containing a stack-trace of the location where a test failed.
* **Containing Elements:** [&lt;failure&gt;](#failure)
* **Contained Elements:** None
* **Attributes: None

##&lt;output&gt;
Optional element that appears on tests or suites that produce text output. The output may be intercepted from writes to the console or captured directly when the test writes to the TestContext. It is contained in a CDATA section.
 * **Containing Elements:** [&lt;test-suite&gt;](#test-suite), [&lt;test-case&gt;](#test-case)
 * **Contained Elements:** None
 * **Attributes: None
