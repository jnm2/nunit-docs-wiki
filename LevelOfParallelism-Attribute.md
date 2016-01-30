This is an _assembly-level_ attribute, which may be used to specify the level of 
parallelism, that is, the maximum number of worker threads executing tests in the assembly.
It may be overridden using a command-line option in the console runner.

This attribute is optional. If it is not specified, NUnit uses the processor count or 2,
whichever is greater. For example, on a four processor machine the default value is 4.

####Example

The following code, which might be placed in AssemblyInfo.cs, sets the level of parallelism to 3:

```C#
  [assembly:LevelOfParallelism(3)]
```

####See also...
 * [[Parallelizable Attribute]]
