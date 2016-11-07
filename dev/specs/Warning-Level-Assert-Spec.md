Sometimes - especially in integration testing - it's desirable to give a warning message but continue execution. This feature will provide the ability to do so.

###Warning Results

NUnit currently supports four fundamental outcomes, represented by the `TestStatus` enumeration. This change would add a fifth value, `Warning` to the enum:

```C#
    /// <summary>
    /// The TestStatus enum indicates the result of running a test
    /// </summary>
    public enum TestStatus
    {
        /// <summary>
        /// The test was inconclusive
        /// </summary>
        Inconclusive,

        /// <summary>
        /// The test has skipped 
        /// </summary>
        Skipped,

        /// <summary>
        /// The test succeeded
        /// </summary>
        Passed,

        /// <summary>
        /// There was a warning
        /// </summary>
        Warning,

        /// <summary>
        /// The test failed
        /// </summary>
        Failed
    }
```

A new well-known `ResultState` would be created: `ResultState.Warning`. In addition, `ResultState.Ignored`, which is currently defined as "Skipped:Ignored" but specially handled as a warning, would be redefined as "Warning:Ignored". This would have the side effect that coloring of output would then completely follow the `TestStatus`, without any exceptions.

All switches and tests on `TestStatus` or `ResultState` would need to be examined and have code added to deal with warnings. If we decide to proceed with this, it's probably best to make these internal changes before moving on to the explicit syntax for warnings.

### Syntax

In the NUnit framework, Constraints either succeed, fail or throw an unexpected exception. ConstraintResults therefore have a status of "Success", "Failure" or "Error". It's up to the individual assertion verbs to decide how to interpret a "Failure" status. For example, `Assert.That` causes the test to fail, while `Assume.That`causes the test to be inconclusive.

In keeping with the overall design, we will need a new assertion verb to return a warning when the associated constraint fails. There are a number of candidates, as seen in these examples:

```C#
  // Use Check - used in some versions of cppunit and in boost
  Check.That(2+2 == 5);
  Check.That(2+2, Is.EqualTo(5));
  Check.That(() => 2+2, Is.EqualTo(5).After(3000));

  // Use Expect - used in gtest in this way, but may conflict with AssertionHelper
  Expect.That(2+2 == 5);
  Expect.That(2+2, Is.EqualTo(5));
  Expect.That(() => 2+2, Is.EqualTo(5).After(3000));

  // Use Warn with reversed condition - Warn.If could be used the same way
  Warn.That(2+2 != 5);
  Warn.That(2+2, Is.Not.EqualTo(5));
  Warn.That(() => 2+2, Is.Not.EqualTo(5).After(3000));

  // Use Warn with original condition
  Warn.Unless(2+2 == 5);
  Warn.Unless(2+2, Is.EqualTo(5));
  Warn.Unless(() => 2+2, Is.EqualTo(5).After(3000));
```

All of the above items would fail - even the one that waits 3 seconds. :-) The test would continue to execute, however, and the warning messages would be reported at the end of the test. The feature would inter-operate with `Assert.Multiple` and any warning assertions would be listed along with failed assertions that occurred in an `Assert.Multiple` block.

Additionally, we would want to implement `Assert.Warn` giving an absolute way to issue a warning, similar to `Assert.Pass` and `Assert.Fail`.

Selection of the exact syntax is the main issue blocking implementation.