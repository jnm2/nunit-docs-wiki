###DRAFT - Partially Implemented

This feature is inspired by MbUnit's **Assert.Multiple**. It allows the user to review multiple failures in one run of the test and is useful for testing things like object initialization and UI appearance. It is likely to have the greatest use in extremely simple unit tests and in integration testing.

In order to report multiple assertion results against a single test, the format of the test result XML would need to be enhanced. This  is covered in the first major section below.

We would implement the same syntax, but not necessarily identical semantics, as used by NUnit. The implementation itself would be different, since the underlying structure of the NUnit framework differs from that of MbUnit. This is covered below, in the the second major section.

##XML Result Representation

###Current Elements

Currently, only the assertion that terminates a test is shown in the XML. This may be a failure encountered in the course of a normal assert. Or a "categorical" assert such as `Assert.Fail`, `Assert.Success`, `Assert.Ignore` or `Assert.Inconclusive`.

The following elements are currently used in the XML:

####`<failure>`
This element appears when a test has failed or an unexpected exception has occured. It contains sub-elements for the message and stack trace.

####`<reason>`
This element appears when a test has been skipped or ignored for some reason. It contains a message element.

###Enhanced Elements

The test case could potentially contain an entry for each assertion executed, although the initial implementation would only include multiple failing asserts in support of this specification. The enhanced elements would be contained in an `<asserts>` element as follows:

```xml
            <asserts>
              <assert result="failed">
                <message>Assert message 1</message>
                <stack-trace>...</stack-trace>
              </assert result="failed">
              <assert result="failed">
                <message>Assert message 2</message>
                <stack-trace>...</stack-trace>
              </assert>
            </asserts>
```

Each individual assertion result would normally include a message and stacktrace, duplicating what is generally contained in the existing `<failure>` element. The `result` attribute would always be set to failed in the initial implementation, since only failures are shown but could be expanded as the feature was used for other purposes to include values of 'warning' and 'passed' for example.

###Compatibility

For backward compatibility, a failure in the multiple assert block would cause a special message to be generated, concatenating all the individual failure messages. The stack trace would show the point of exit from the block.

##Assert.Multiple Syntax

Here is an example of using **Assert.Multiple**:

![Assert.Multiple](https://cloud.githubusercontent.com/assets/8772586/5229921/014e331e-76e4-11e4-8f94-45a553b75faf.png)

Functionally, this results in NUnit storing any failures encountered in the block and reporting all of them together upon exit of the block. The test itself would terminate at the end of the block if any failures were encountered, but would continue otherwise.

###Unexpected Exceptions

The test will be terminated immediately if any exception is thrown that is not handled by the test. An unexpected exception is often an indication that the test itself is in error, so it must be terminated.

If the exception occurs after one or more assertion failures have been recorded, those failures will be reported along with the terminating exception itself.

###Special Asserts

**Assert.Fail**, **Assert.Pass**, **Assert.Inconclusive** and **Assert.Ignore** normally cause the test to terminate immediately with result states of Failure, Success, Inconclusive and Ignored respectively. Each of these could conceivably be handled in one of two different ways:
 1. Immediately terminate the test with an error if they are found in any multiple assert block. The error would cause this to be handled as an unexpected exception.
 2. Like option 1, but only report an error if failures have already been recorded in the block. This may be preferred to option 1, since some users may call methods containing assertions from inside a multiple assert block. The method would not necessarily know that it was running inside a block.
 3. Record the result as pending until the end of the block and then terminate the test using the "worst" of the results encountered. This is slightly more complicated but may be easier to explain to users, since all asserts will work the same way.

Specific behavior to use in each case follows:

####Assert.Fail

Assert.Fail should be handled just as any other assert failure. The message and stack trace will be recorded but the test will continue to execute until the end of the block. This is necessary because Assert.Fail is sometimes used in place of a more normal assert, in order to tailor the message.

####Assert.Pass / Assert.Ignore / Assert.Inconclusive / Assume.That

Report an error if any of these is used inside a multiple assert block (option 1). While it's possible to use option 3 here, the use of these asserts inside a multiple assert block doesn't really make much sense. Note that we can change our mind later and use option 3 if it should be needed. Going from 3 to 1 or 2 would not be popular since it would remove functionality.

Originally, the plan was to allow assumptions inside a multiple assert block. However, in practice, this is somewhat complicated, since the block could have both assumptions and assertions. A failed assumption is intended to terminate the execution of a block.

###Effect on Third-Party Frameworks

Some third-party assertion frameworks actually throw an NUnit AssertionException on failure. Such frameworks should automatically work in concert with the multiple assertion feature.

Other frameworks, particularly mock frameworks, throw a "foreign" exception. These exceptions are already treated as errors rather than failures by NUnit. This will continue to be the case and the foreign exceptions will terminate the test immediately.

While this is not a change in behavior, the presence of a new feature, which is not accessible to third party frameworks may lead to a desire to integrate some frameworks more closely. There are several ways this can be done, some requiring changes to NUnit while others can be implemented by the third-party framework.

At the moment, we don't know what frameworks are affected. It's speculated that this is less of a problem for a mock framework than for an assertion framework, since failure of a mock expectation normally terminates a test. At any rate, the initial implementation of this feature will probably lead to additional enhancement requests.

###Not Being Implemented

MbUnit also has a **MultipleAssertsAttribute**, which we don't plan to implement at this time.

![MultipleAssertsAttribute](https://cloud.githubusercontent.com/assets/8772586/5229899/cea342e2-76e3-11e4-9d00-3661971d2b8f.png)

This functions identically to **Assert.Multiple**. The entire test runs as if its body were enclosed in an **Assert.Multiple** block.

We have no plans to implement this attribute but could reconsider later on if there is a demand for it.
