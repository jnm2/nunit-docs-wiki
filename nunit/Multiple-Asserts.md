Usually, once an assertion fails, we want the test to terminate. But sometimes, it's desireable to continue and accumulate any additional failures so they may all be fixed at once. This is particularly useful for testing things like object initialization and UI appearance as well as certain kinds of integration testing.

###Syntax

Multiple asserts are implemented using the `Assert.Multiple` method. Here is an example of its use:

```C#
[Test]
public void ComplexNumberTest()
{
    ComplexNumber result = SomeCalculation();

    Assert.Multiple(() =>
    {
        Assert.AreEqual(5.2, result.RealPart, "Real part");
        Assert.AreEqual(3.9, result.ImaginaryPart, "Imaginary part");
    });
}
```

Functionally, this results in NUnit storing any failures encountered in the block and reporting all of them together upon exit from the block. If both asserts failed, then both would be reported. The test itself would terminate at the end of the block if any failures were encountered, but would continue otherwise.

####Notes:

1. The multiple assert block may contain any arbitrary code, not just asserts.

2. Multiple assert blocks may be nested. Failure is not reported until the  outermost block exits.

3. If the code in the block calls a method, that method may also contain multiple assert blocks.

4. The test will be terminated immediately if any exception is thrown that is not handled. An unexpected exception is often an indication that the test itself is in error, so it must be terminated. If the exception occurs after one or more assertion failures have been recorded, those failures will be reported along with the terminating exception itself.

5. Assert.Fail is handled just as any other assert failure. The message and stack trace are recorded but the test continues to execute until the end of the block.

6. An error is reported if any of the following are used inside a multiple assert block:
   * Assert.Pass
   * Assert.Ignore
   * Assert.Inconclusive
   * Assume.That

7. Use of Warnings (Assert.Warn, Warn.If, Warn.Unless) is permitted inside a multiple assert block. Warnings are reported normally along with any failures that occur inside the block.

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

