Sometimes - especially in integration testing - it's desirable to give a warning message but continue execution. NUnit supports this with the `Warn` class and the `Assert.Warn` method.

###Syntax

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

Each of the above items would fail. The test would continue to execute, however, and the warning messages would only be reported at the end of the test. If the test subsequently fails, the warnings will be displayed along with the failure message or - in the case of `Assert.Multiple` - messages.