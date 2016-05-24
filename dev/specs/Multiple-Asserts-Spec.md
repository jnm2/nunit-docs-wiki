###DRAFT - Not Yet Implemented

This feature is inspired by MbUnit's **Assert.Multiple** and **MultipleAssertsAttribute**. It allows the user to review multiple failures in one run of the test and is useful for testing things like object initialization and UI appearance. It is likely to have the greatest use in extremely simple unit tests and in integration testing.

We would implement the same syntax, but not necessarily identical semantics, because there are some issues of how it would interact with other NUnit features. The implementation itself would be different, since the underlying structure of the NUnit framework differs from that of MbUnit.

###Assert.Multiple

Here is an example of using **Assert.Multiple**:

![Assert.Multiple](https://cloud.githubusercontent.com/assets/8772586/5229921/014e331e-76e4-11e4-8f94-45a553b75faf.png)

Functionally, this results in NUnit storing any failures encountered in the block and reporting all of them together upon exit of the block. The test itself would terminate at the end of the block if any errors were encountered, but would continue otherwise.

###MultipleAssertsAttribute

Here is an example of using the **MultipleAssertsAttribute**:

![MultipleAssertsAttribute](https://cloud.githubusercontent.com/assets/8772586/5229899/cea342e2-76e3-11e4-9d00-3661971d2b8f.png)

This functions identically to **Assert.Multiple**. The entire test runs as if its body were enclosed in an **Assert.Multiple** block.

###Early Termination

The test will be terminated immediately if any of the following events occur:

  * Execution of **Assert.Fail**, **Assert.Pass**, **Assert.Inconclusive** or **Assert.Ignore**.
  * Failure of any Assumption (**Assume.That**), which is equivalent to **Assert.Inconclusive**.

If any of  the events causing early termination occur, it's possible to have a conflict. For example, if there are pending failures and the user executes **Assert.Pass** we have to decide whether to report the test as a failure or a success. Since failure to report failures is a cardinal sin for a testing framework, we will always report failure. In each case, an **additional** failure message will be added to the list of pending failures before terminating.

The following table shows the general form of message that will be used in the case of each early termination event:

| Event | Message |
|-------|--------|
| **Assert.Fail**          | Assert.Fail encountered with pending failures: $usermessage$ |
| **Assert.Pass**          | Assert.Pass encountered with pending failures: $usermessage$ |
| **Assert.Inconclusive**  | Assert.Inconclusive encountered with pending failures: $usermessage$ |
| **Assert.Ignore**        | Assert.Ignore encountered with pending failures: $usermessage$ |
| Failing **Assume.That**  | Assumption failed with pending test failures: $usermessage$ |
