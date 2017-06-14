This attribute is to identify methods that are called once prior to executing any of the tests
in a fixture. It may appear on methods of a TestFixture or a SetUpFixture.

OneTimeSetUp methods may be either static or
instance methods and you may define more than one of them in a fixture.
Normally, multiple OneTimeSetUp methods are only defined at different levels
of an inheritance hierarchy, as explained below.

If a OneTimeSetUp method fails or throws an exception, none of the tests
in the fixure are executed and a failure or error is reported.

#### Example:

```C#
namespace NUnit.Tests
{
  using System;
  using NUnit.Framework;

  [TestFixture]
  public class SuccessTests
  {
    [OneTimeSetUp]
    public void Init()
    { /* ... */ }

    [OneTimeTearDown]
    public void Cleanup()
    { /* ... */ }

    [Test]
    public void Add()
    { /* ... */ }
  }
}
```

### Inheritance

The OneTimeSetUp attribute is inherited from any base class. Therefore, if a base
class has defined a OneTimeSetUp method, that method will be called
before any methods in the derived class.

You may define a OneTimeSetUp method
in the base class and another in the derived class. NUnit will call base
class OneTimeSetUp methods before those in the derived classes.

#### Notes:

 1. Although it is possible to define multiple OneTimeSetUp methods
    in the same class, you should rarely do so. Unlike methods defined in
    separate classes in the inheritance hierarchy, the order in which they
    are executed is not guaranteed.

 2. OneTimeSetUp methods may be async if running under .NET 4.0 or higher.


#### See also...
 * [[SetUp Attribute]]
 * [[TearDown Attribute]]
 * [[OneTimeTearDown Attribute]]
