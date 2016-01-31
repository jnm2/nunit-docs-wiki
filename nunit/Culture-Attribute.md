<p>The Culture attribute is used to specify cultures for which a test or fixture
	should be run. It does not affect the culture setting, but merely uses it to 
	determine whether to run the test. If you wish to change the culture when
	running a test, use the SetCulture attribute instead.</p>
	
<p>If the specified culture requirements for a test are not met it is skipped.
   In the gui, the tree node for the test remains gray and the status bar color is 
   not affected.</p>

<p>One use of the Culture attribute is to provide alternative tests under different
cultures. You may specify either specific cultures, like "en-GB" or neutral
cultures like "de".</p>

<h4>Test Fixture Syntax</h4>

```C#
namespace NUnit.Tests
{
  using System;
  using NUnit.Framework;

  [TestFixture]
  [Culture(&quot;fr-FR&quot;)]
  public class FrenchCultureTests
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
    [Culture(Exclude=&quot;en,de&quot;)]
    public void SomeTest()
    { /* ... */ }
}
```

<h4>See also...</h4>
 * [[SetCulture Attribute]]

