<p>This attribute is to identify methods that are called once after executing all the tests
	in a fixture. It may appear on methods of a TestFixture or a SetUpFixture.
	
<p>OneTimeTearDown methods may be either static or
   instance methods and you may define more than one of them in a fixture.
   Normally, multiple OneTimeTearDown methods are only defined at different levels
   of an inheritance hierarchy, as explained below.

<p>So long as any OneTimeSetUp method runs without error, the OneTimeTearDown method is 
   guaranteed to run. It will not run if a OneTimeSetUp method fails or throws an 
   exception.</p>

<h4>Example:</h4>

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

<h3>Inheritance</h3>

<p>The OneTimeTearDown attribute is inherited from any base class. Therefore, if a base 
	class has defined a OneTimeTearDown method, that method will be called 
	after any test methods in the derived class. 
	
<p>You may define a OneTimeTearDown method
   in the base class and another in the derived class. NUnit will call base
   class OneTimeTearDown methods after those in the derived classes.
   
<h4>Notes:</h4>
<ol>
<li>Although it is possible to define multiple OneTimeTearDown methods
   in the same class, you should rarely do so. Unlike methods defined in
   separate classes in the inheritance hierarchy, the order in which they
   are executed is not guaranteed.
<li>OneTimeTearDown methods may be async if running under .NET 4.0 or higher.
</ol>

<h4>See also...</h4>
 * [[SetUp Attribute]]
 * [[TearDown Attribute]]
 * [[OneTimeSetUp Attribute]]
 * [[TestFixture Attribute]]
 * [[SetUpFixture Attribute]]
