**TestFixtureSourceAttribute** is used on a parameterized fixture to
identify the source from which the required constructor arguments will be provided.
The data is kept separate from the fixture itself and may be used by multiple
fixtures. See [[Parameterized Tests]] for a general introduction to
tests with arguments.

####Usage

Consider a test fixture class taking two parameters in its constructor, a string and an int. We can specify the test and it's data using one of the forms of **TestFixtureSourceAttribute**:

######Form 1 - [TestFixtureSource(string sourceName)]

```C#
[TestFixtureSource("FixtureArgs")]
public class MyTestClass
{
    public MyTestClass(string word, int num) { ... }

    ...

    static object [] FixtureArgs = {
        new object[] { "Question", 1 },
        new object[] { "Answer", 42 }
    };
}
```

The single attribute argument in this form is a string representing the name of the source used
to provide arguments for constructing the TestFixture. It has the following characteristics:

 * It may be a field, property or method in the test class.

 * It __must__ be static.

 * It must return an IEnumerable or a type that implements IEnumerable. For fields an array is generally used. For properties and methods, you may return an array or implement your own iterator.

 * The individual items returned by the enumerator must either be object arrays or implement ITestFixtureData.
   Arguments must be consistent with the fixture constructor.

######Form 2 - [TestFixtureSource(Type sourceType, string sourceName)]

```C#
[TestFixtureSource(typeof(AnotherClass), "FixtureArgs")]
public class MyTestClass
{
    public MyTestClass(string word, int num) { ... }

    ...
}

class AnotherClass
{
    static object [] FixtureArgs = {
        new object[] { "Question", 1 },
        new object[] { "Answer", 42 }
    };
}
```

The first argument of the attribute in this form is a Type representing the class that will provide
the test fixture data.

The second argument is a string representing the name of the source used
to provide test fixtures. It has the following characteristics:

 * It may be a field, property or method in the test class.

 * It __must__ be static.

 * It must return an IEnumerable or a type that implements IEnumerable. For fields an array is generally used. For properties and methods, you may return an array or implement your own iterator.

 * The individual items returned by the enumerator must either be object arrays or implement ITestFixtureData.
   Arguments must be consistent with the fixture constructor.

######Form 3 - [TestFixtureSource(Type sourceType)]

```C#
[TestFixtureSource(typeof(FixtureArgs))]
public class MyTestClass
{
    public MyTestClass(string word, int num) { ... }

    ...
}

class FixtureArgs: IEnumerable
{
    public IEnumerator GetEnumerator()
    {
        yield return new object[] { "Question", 1 };
        yield return new object[] { "Answer", 42 };
    }
}
```

The Type argument in this form represents the class that provides test cases.
It must have a default constructor and implement <b>IEnumerable</b>. 

The individual items returned by the enumerator must either be object arrays or implement ITestFixtureData.
Arguments must be consistent with the fixture constructor.

####Named Parameters

TestCaseSourceAttribute supports one named parameter:

 * **Category** is used to assign one or more categories to every test case returned from this source.

####Test Case Construction

In constructing tests, NUnit uses each item returned by
the enumerator as follows:

1. If it is an object implementing `NUnit.Framework.ITestCaseData`, 
   its properties are used to provide the test case. NUnit provides
   the [[TestCaseData]] type for this purpose.

3. If it is an <b>object[]</b>, its members are used to provide
   the arguments for the method. This is the approach taken in
   the three examples above.

#####Notes:

1. It is recommended that the SourceType not be the same as the test fixture class. It may be a nested class, however, and probably should be if the data is only used within that fixture.

2. A generic IEnumerable and IEnumerator may be used but NUnit will actually deal with the underlying IEnumerator in the current release.

3. The GetEnumerator method may use yield statements or simply return the enumerator for an array or other collection held by the class.

####Order of Execution

Individual test cases are 
executed in the order in which NUnit discovers them. This order does <b>not</b>
follow the lexical order of the attributes and will often vary between different
compilers or different versions of the CLR.
   
As a result, when <b>TestCaseSourceAttribute</b> appears multiple times on a 
method or when other data-providing attributes are used in combination with 
<b>TestCaseSourceAttribute</b>, the order of the test cases is undefined.

However, when a single <b>TestCaseSourceAttribute</b> is used by itself, 
the order of the tests follows exactly the order in which the test cases 
are returned from the source.
   
####Object Construction

NUnit locates the test cases at the time the tests are loaded. It creates
instances of each class used with the third form of the attribute and builds a list of 
tests to be executed. Each data source class is only created once at this
time and is destroyed after all tests are loaded. By design, no communication is
possible between the load and execution phases except through the tests that
are created.

