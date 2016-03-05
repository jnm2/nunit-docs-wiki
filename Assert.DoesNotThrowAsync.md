<b>Assert.DoesNotThrowAsync</b> verifies that the delegate provided as an argument 
does not throw an exception. See [[Assert.DoesNotThrow]] for synchronous code.

```C#
void Assert.DoesNotThrowAsync( AsyncTestDelegate code );
void Assert.DoesNotThrowAsync( AsyncTestDelegate code, 
                          string message, params object[] parms);
```

<h4>See also...</h4>
 * [[Assert.ThrowsAsync]]
 * [[ThrowsConstraint]]
