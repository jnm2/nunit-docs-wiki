The NUnit Test Engine uses a plugin architecture to allow new functionality to be added by third parties. We originally planned to use `Mono.Addins` for this purpose and did so in the first betas. Because `Mono.Addins` no longer supports .NET 2.0, we were using a modified version that we created ourselves and which we would have to maintain in the future. Since `Mono.Addins` has many more features than we expect to use we decided to return to a custom plugin architecture.

The NUnit 3.0 Engine Extensibility model is essentially based on the NUnit V2 addin design with a number of improvements, primarily inspired by `Mono.Addins`. On this page, we describe that model as a guide for folks working on NUnit or otherwise needing to understand it. See [[Writing Engine Extensions]] for user-focused informaton about how to create an extension.

##Extension Points

NUnit 3.0 Extensibility centers around `ExtensionPoints`. 

####Supported Extension Points

As of NUnit 3.2, the following extension types are supported:

* [[Project Loaders]]
* [[Result Writers]]
* [[Framework Drivers]]
* [[Event Listeners]]

##Extensions

An `Extension` is a single object of the required `Type`, which is registered with an `ExtensionPoint`. Extensions are identified by the `ExtensionAttribute` and additional information may be provided by use of the `ExtensionPropertyAttribute`, both of which are applied to the class that implements the extension.

All `Extensions` must have a default constructor, which is used by NUnit to create the object when it is needed.

####ExtensionAttribute

The `ExtensionAttribute` has only a default constructor, as well as two named properties, `Path` and `Description`. If the path is not provided, NUnit will try to find the appropriate extension point based on what Types are inherited or implemented by the class on which the attribute is placed.

Assuming the extension point definition used above, any of the following would identify the classes as driver factories.

```C#
    [Extension(Path = "/NUnit/Engine/TypeExtensions/IDriverFactory")]
    public class DriverFactory1 : IDriverFactory
    {
        ...
    }

    [Extension]
    public class DriverFactory2 : IDriverFactory
    {
        ...
    }
```

Generally, the `Path` will be omitted and the default value used. It may be needed in some cases, where classes implement multiple interfaces or inherit other classes that do so. Usually, this is not necessary if you follow the Single Responsibility principle.

####ExtensionPropertyAttribute

Using only the `ExtensionAttribute`, NUnit would have to create instances of every extension in order to query it (for example) about its capabilities. Since extensions are generally in separate assemblies, this means that many potentially unneeded assemblies would be loaded.

The `ExtensionPropertyAttribute` avoids this problem by allowing the extension to specify information about what it is able to do. NUnit scans the attributes using `Mono.Cecil` without actually loading the assembly, so that resources are not taken up by unused assemblies.

To illustrate this, we will use the example of the engine's project loader `ExtensionPoint`. You can read about this extension point in detail at [[Project-Loaders]] but the essential thing for this example is that the extension point is passed a file path and must determine whether that file is in a format that it can interpret and load. We do that by loading the extension and calling its `CanLoadFrom(string path)` method.

If we only knew what file extensions were used by the particular format, we could avoid loading the extension unnecessarily. That's where `ExtensionPropertyAttribute` comes in. The following is an example taken from NUnit's own extension for loading NUnit projects.

```C#
    [Extension]
    [ExtensionProperty("FileExtension", ".nunit")]
    public class NUnitProjectLoader : IProjectLoader
    {
        ...
    }
```
By use of the `ExtensionPropertyAttribute` the assembly containing this extension will never be loaded unless the user asks NUnit to run tests in a file of type `.nunit`. If this attribute were not present, then the engine would have to load the assembly, construct the object and call its `CanLoadFrom` method.

Of course, this means that the extension author must know a great deal about how each extension point works. That's why we provide a page for each supported extension points with details of how to use it.
