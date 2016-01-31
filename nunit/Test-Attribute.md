The Test attribute is one way of marking a method inside a TestFixture class
as a test. It is normally used for simple (non-parameterized) tests but may
also be applied to parameterized tests without causing any extra test cases
to be generated. See [[Parameterized Tests]] for more info.

The test method may be either an instance or a static method.
   
Test methods targetting .Net 4.0 or higher may be 
marked as <b>async</b> and NUnit will wait for the method to complete 
before recording the result and moving on to the next test. Async
test methods must return `Task` if no value is returned,
or `Task<T>` if a value of type T is returned.
	
If the programmer marks a test method that does not have the correct signature 
it will be considered as not runnable and be indicated as such by the console
or gui runner. In the Gui, such tests are marked in red.
  
If the test method returns a value, you must pass in the expected result as
a named parameter to the Test attribute. This expected return value will be
checked for equality with the return value of the test method.
   
####Examples:

```C#
namespace NUnit.Tests
{
  using System;
  using NUnit.Framework;

  [TestFixture]
  public class SuccessTests
  {
    // A simple test
    [Test]
    public void Add()
    { /* ... */ }

    // A simple async test
    [Test]
    public async Task AddAsync()
    { /* ... */ }
   
    // Test with an expected result
    [Test(ExpectedResult = 4)]
    public int TestAdd()
    {
        return 2 + 2;
    }
   
    // Async test with an expected result
    [Test(ExpectedResult = 4)]
    public async Task<int> TestAdd()
    {
        await ...
        return 2 + 2;
    }
  }
}
```
