###DRAFT - Not Yet Implemented

Sometimes - especially in integration testing - it's desirable to give a warning message but continue execution. This feature will provide the ability to do so.

### Check.That

A new static class will be added to the framework. The name **Check** is preliminary. Other possibilities are **Verify** and **Warn** - but see the note below about **Warn**.

**Check.That** would support all the same uses as **Assert.That** and **Assume.That**, for example...

```C#
  Check.That(2+2 == 5);
  Check.That(2+2, Is.EqualTo(5));
  Check.That(() => 2+2, Is.EqualTo(5).After(3000));
```

All of the above items would fail - even the one that waits 3 seconds. :-) The test would continue to execute, however, and the warning messages would be reported at the end of the test. If the test were to be terminated early by some sort of failure, the warnings would be reported in addition to the ultimate failure.

**Note:** If instead of **Check** we use **Warn** there are two alternatives. Either the condition has to be reversed or the following verb must be changed. For example,

```C#
  Warn.That(2+2, Is.Not.EqualTo(5));
  Warn.Unless(2+2, Is.EqualTo(5));
```

Both of the above usages seem confusing. Perhaps other alternatives can be examined.

###Warning Results

If a test runs without failures, but with warnings, we will need a new ResultState to represent the outcome. There are two possibilities to choose from:

1. Add **Warning** as a member of **TestStatus**, giving us five rather than four fundamental outcomes. This would involve changes in lots of places upon implementation, but would leave us with a fairly simple interpretation of results. Among other things, we would probably want to add a warnings attribute to the XML representation of test suite results.

2. Create a new well-known **ResultState**, without adding to **TestStatus**. This could be either **Failed:Warning** or **Passed:Warning** depending on how we want to look at it. I lean towards the former, because it keeps the **Passed** state clean - their are currently know sub-categories of **Passed**.

If we take the second approach, we may want to add an explicit **Severity** to **ResultState** so as to simplify processing of results for clients. That too would need to be added to the Xml.

###Ignored Tests

If we implement warnings, then Ignored results should become a type of warning result: **Warning:Ignored** rather than **Skipped:Ignored**.

###Decisions Pending

We need to decide, in priority order:

1. Whether to do this at all.

2. What syntax to use.

3. What representation to use for the result internally.

###Implementation

Once the decisions are made, implementation should be fairly straightforward. We will need a central place to collect warnings, which can be a collection in the **TestExecutionContext**. We will want to centralize result reporting in Assert as well, rather than throwing exceptions from multiple locations.

This feature needs to be coordinated with [[Multiple Asserts]].

