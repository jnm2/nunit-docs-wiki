> **NOTE:** This page is a specification that was used as a starting point for creating the feature in NUnit. It needs to be reviewed and revised in order to accurately reflect what was actually built. If you take it with a grain of salt, it may still be helpful to you as documentation. This notice will be removed when the page is brought up to date.

When the NUnit Console Runner is executed with the `--teamcity` option or when it is started under the TeamCity NUnit build step, the special messages described below are printed to the standard output. The messages are intercepted by TeamCity to show progress as the test executes.

When a test starts, the following message appears in the standard output stream:
<br>
`##teamcity[testStarted name='TestName' captureStandardOutput='true' flowId='FlowId']`
* The `name` attribute contains the test name, for example: `NUnit.Engine.Services.Tests.CoreTestRunnerFactoryTests.ServiceIsStarted`.
* The `captureStandardOutput` attribute shows that all standard output (and standard error) messages received between the `testStarted` and closing messages will be considered as the test output. 
* The `flowId` attribute is used when a test works concurrently with other tests to have a consistent view of the result.

When a test is finished successfully, the standard output contains the following message: 
<br>
`##teamcity[testFinished name='TestName' duration='Duration' flowId='FlowId']`. 

* The `duration` attribute shows the test duration.

When a test fails, the standard output contains an additional message before `testFinished`: 
<br>
`##teamcity[testFailed name='TestName' message='Message' details='Stack trace' flowId='FlowId']`. 
* The `message` attribute contains the error message.
* The `details` attribute  contains the detailed error information, usually  a stack trace.

When a test is ignored or has the  "Inconclusive" state, the `testFinished` service message  is replaced with the `testIgnored` service message : 
<br>
`##teamcity[testIgnored name='TestName' message='message' flowId='FlowId']`