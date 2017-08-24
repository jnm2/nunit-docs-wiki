This attribute is used to indicate whether the test and/or its descendants may be run in parallel with other tests. By default, no parallel execution takes place.

The constructor takes an optional **ParallelScope** enumeration argument (see below), which defaults to **ParallelScope.Self**. The attribute may be used at the assembly, class or method level and the word "test" in the rest of this description refers to the suite or test case that corresponds to the item on which the attribute appears.

#### ParallelScope Enumeration

This is a **[Flags]** enumeration used to specify which tests may run in parallel. It applies to the test upon which it appears and any subordinate tests. It is defined as follows:
```C#
[Flags]
public enum ParallelScope
{
    None,     // the test may not be run in parallel with other tests
    Self,     // the test itself may be run in parallel with other tests
    Children, // child tests may be run in parallel with one another
    Fixtures  // fixtures may be run in parallel with one another
}
```

#### Notes:

 1. Parallel execution of methods within a class is supported starting with NUnit 3.7. In earlier releases, parallel execution only applies down to the TestFixture level, `ParallelScope.Children` works as `ParallelScope.Fixtures` and any `ParallelizableAttribute` placed on a method is ignored.

 2. Values that apply to a higher level test than the test on which the scope appears - for example, ParallelScope.Fixtures appearing on a method - are ignored without warning or affect.

 3. Although `ParallelScope.None` continues to be supported, it is recommended that you use the new [[NonParallelizable Attribute]] in new work.

#### Specifying Parallelizable at Multiple Test Levels

The **ParallelizableAttribute** may be specified on multiple levels of the tests. Settings at a higher level may affect lower level tests, unless those lower-level tests override the inherited settings. Thus, if the assembly has **ParallelScope.None** either by use of the attribute or by default, classes with **ParallelScope.Self** may be run in parallel as may their children if an appropriate scope is used.

Note that a lower-level test cannot change the settings on higher-level tests. Thus, allowing parallel execution for methods of a class that does not allow it, results in those methods running in parallel with one another, but not in parallel with test methods under any other classes. This is the natural outcome of the fact that the execution of a test method is, in fact, part of the execution of the test represented by the class.

#### See also...
 * [[NonParallelizable Attribute]]
 * [[LevelOfParallelism Attribute]]

