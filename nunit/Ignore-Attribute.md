**IgnoreAttribute** is used to indicate that a test should not be executed for
some reason. Note that with NUnit 3.0, the reason must be specified. Ignored 
tests are displayed by the runners as warnings in order to provide a reminder
that the test needs to be corrected or otherwise changed and re-instated.

####Test Fixture Syntax

```C#
namespace NUnit.Tests
{
  using System;
  using NUnit.Framework;

  [TestFixture]
  [Ignore("Ignore a fixture")]
  public class SuccessTests
  {
    // ...
  }
}
```

<h4>Test Syntax</h4>

```C#
namespace NUnit.Tests
{
  using System;
  using NUnit.Framework;

  [TestFixture]
  public class SuccessTests
  {
    [Test]
    [Ignore("Ignore a test")]
    public void IgnoredTest()
    { /* ... */ }
}
```

####Ignore Until

The `Until` named parameter allows you to ignore a test for a specific period of time,
after which the test will run normally. The until date must be a string
that can be parsed to a date.

```C#
[TestFixture]
[Ignore("Waiting for Joe to fix his bugs", Until = "2014-07-31 12:00:00Z"]
public class MyTests
{
 [Test]
 public void Test1() { /* ... */ }
}
```

In the above example, it's assumed that the test would fail if run. With the
IgnoreAttribute, it will give a warning until the specified date. After that
time, it will run normally and either pass or fail.