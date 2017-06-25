This interface is used by attributes that know how to build a fixture from a user class. `IFixtureBuilder` is defined as follows:

```C#
public interface IFixtureBuilder
{
    TestSuite BuildFrom(Type type);
}
```

Custom fixture builders should examine the provided Type and return an appropriate TestFixture based on it. If the fixture is intended to be an NUnit TestFixture, then the helper class `NUnitTestFixtureBuilder` may be used to create it.

The following NUnit attributes currently implement this interface:
* `TestFixtureAttribute`
* `SetUpFixtureAttribute`

> It would make more sense for this interface method to return `TestFixture` rather than `TestSuite`. We use `TestSuite` because it is the common base for both `TestFixture` and `SetupFixture`. In a future version, we will try to adjust the hierarchy so that all suites based on a class are derived from `TestFixture`.

