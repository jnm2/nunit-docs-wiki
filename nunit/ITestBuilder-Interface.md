This interface is used by attributes that know how to build one or more parameterized `TestMethod` instances from a `MethodInfo`. `ITestMethodBuilder` is defined as follows:

```C#
public interface ITestBuilder
{
    IEnumerable<TestMethod> BuildFrom(MethodInfo method, Test suite);
}
```

Custom attributes implementing this interface should examine the MethodInfo and return as many `TestMethod` instances as it is able to construct, using the parameters available to it. Some attributes will only return a single test, just as `TestCaseAttribute` does. Others, working like `TheoryAttribute` may return multiple tests. If no data is available to create tests, an empty collection should be returned. 

If the returned tests are standard NUnit TestMethods, the helper class `NUnitTestCaseBuilder` may be used to create them. 

The following NUnit attributes currently implement `ITestBuilder`:
* `CombiningStrategyAttribute`, with the following derived classes:
  * `CombinatorialAttribute`
  * `PairwiseAttribute`
  * `SequentialAttribute`
* `TestCaseAttribute`
* `TestCaseSourceAttribute`
* `TheoryAttribute`

