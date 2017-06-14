The **Author** Attribute adds information about the author of the tests. It can be applied to test fixtures and to tests.

The constructor takes the name of the test author and optionally the author's email address. Author can also be specified on
a TestFixture or Test attribute.

```C#
[TestFixture]
[Author("Jane Doe", "jane.doe@example.com")]
public class MyTests
{
 [Test]
 public void Test1() { /* ... */ }

 [Test]
 [Author("Joe Developer")]
 public void Test2() { /* ... */ }
}

[TestFixture(Author = "Jane Doe")]
public class MyOtherTests
{
 [Test]
 public void Test1() { /* ... */ }

 [Test(Author = "Joe Developer")]
 public void Test2() { /* ... */ }
}
```

**Note:** you can currently only have one Author attribute per fixture or test.