**Assert.False** and **Assert.IsFalse** test that the specified condition is false.
The two forms are provided for compatibility with past versions of NUnit and
NUnitLite.

```C#
Assert.False( bool condition );
Assert.False( bool condition, string message, params object[] parms );

Assert.IsFalse( bool condition );
Assert.IsFalse( bool condition, string message, params object[] parms );
```

#### See also...
 * [Condition Constraints](Constraints#condition-constraints)
