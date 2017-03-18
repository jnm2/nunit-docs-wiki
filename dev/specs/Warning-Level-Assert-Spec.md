Sometimes - especially in integration testing - it's desirable to give a warning message but continue execution. This feature will provide the ability to do so.

### Warning Results

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

In keeping with the overall design, we will need a new assertion verb to return a warning when the associated constraint fails. In this case, two variants are proposed, one using the original condition that is to be tested and one working with a negated condition.

```C#
  // Use Warn with reversed condition
  Warn.If(2+2 != 5);
  Warn.If(2+2, Is.Not.EqualTo(5));
  Warn.If(() => 2+2, Is.Not.EqualTo(5).After(3000));

  // Use Warn with original condition
  Warn.Unless(2+2 == 5);
  Warn.Unless(2+2, Is.EqualTo(5));
  Warn.Unless(() => 2+2, Is.EqualTo(5).After(3000));

  // Issue a warning message
  Assert.Warn("Warning message")
```

All of the above items would fail - even the one that waits 3 seconds. :-) The test would continue to execute, however, and the warning messages would only be reported at the end of the test.

### Reporting

The XML format would be modified to add a `warnings` attribute to each suite, along with the other attributes for each of the possible test statuses. Each warning would add a new `<assertion>` element to the XML with a status of Warning.

The output of nunit3-console and nunitlite will include a count of warnings and display warnings as part of the Errors and Failures report. Warnings should be displayed in the GUI tree using the existing warning-level yellow color.

### Assert.Multiple and Warnings

The feature would inter-operate with `Assert.Multiple` and any warning assertions would be listed along with failed assertions that occurred in an `Assert.Multiple` block. 

The Assert.Multiple feature will have to be modified to recognize which elements in the `<assertions>` display are failures as opposed to warnings and only terminate the test if there are failures.

