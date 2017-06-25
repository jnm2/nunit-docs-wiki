This interface is used by attributes that know how to build a single, non-parameterized test from a `MethodInfo`. `ISimpleTestBuilder` is defined as follows:

```C#
public interface ISimpleTestBuilder
{
    TestMethod BuildFrom(MethodInfo method, Test suite);
}
```

Custom attributes implementing `ISimpleTestFixture` should examine the MethodInfo provided and return a single `TestMethod` instance, as appropriate to that method. The BuildFrom method should never return null, even if the specified method is not valid for a test. In that case, it should return a `TestMethod` with a RunState of NonRunnable, in order to provide feedback to the user who placed the attribute on the method.

NUnit treats attributes implementing this interface specially. They are ignored if any other attributes are present that implement `ITestBuilder`. This allows, for example, use of `[Test]` on a method that also has `[Combinatorial]` specified, without any error arising. Such usage has existed in NUnit for some time and this special handling of the interface allows us to preserve it.

In the current build, only `TestAttribute` implements this interface.

