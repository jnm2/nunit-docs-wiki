The NUnit Test Engine uses a plugin architecture that allows users and third parties to add new functionality to the engine. The extensibility model defines a number of Extension Points to which Extensions may be added. This page is a how-to guide for writing such extensions. For a detailed description of the engine extensibility architechture, see [[Engine Extensibility]].

##Extension Points

NUnit 3.0 Engine Extensibility centers around `ExtensionPoints`, which are defined within the engine itself. Any extension you write must apply to a particular `ExtensionPoint`, so your first task is to decide what kind of extension you will be writing.

The following types of extension are supported in NUnit 3.0:

* **Project Loaders** are extensions that know how to load a project in a particular format and create a package suitable for running tests under NUnit. NUnit itself provides two projet loaders, one to load projects of type `.nunit` and another to load Visual Studio projects and solutions. You would write a project loader extension if you needed to support some other format for storing the names of test assemblies.

* **Result Writers** take the result of a test run, in NUnit 3.0 XML format, and use it to create a result file in some other format. NUnit itself provides three result writers, one to create output in NUnit V2 format, another to write test cases to the console and a third that applies an XML transform to the output. You could write a result writer in order to support an output format of your own choosing.

  **Note:** As an alternative to creating a result writer, you can often use an XML transform to produce the output you desire. Choice of an approach generally comes down to whether you are more comfortable working in XML or a .NET programming language.

* **Framework Drivers** are extensions that know how to load and run tests for a particular framework. The NUnit engine provides drivers for both the NUnit 3.x and NUnit 2.x frameworks. You could write your own framework driver to run tests written against some other framework under NUnit.

* **Event Listeners** are extensions that respond to specific events occuring during the running of a test. They implement the `ITestEventListener` interface. NUnit itself makes extensive use of this interface when running tests.

  **Note:** The ability to create event listener extensions was added to the engine in NUnit 3.4.

##Extension Basics

Extensions are classes implementing a specified interface, depending on the extension point, and marked with the `ExtensionAttribute` in order to be recognized by NUnit. Additional information may be provided by use of the `ExtensionPropertyAttribute`. Specifics for each extension point will be covered below.

Extension classes must have a default constructor, which is used by NUnit to create the object. NUnit creates an instance of the extension only at the time it is actually needed. For example, if the NUnit project loader is installed but no NUnit project is ever loaded, the extension itself is never loaded in memory.

####ExtensionAttribute

The `ExtensionAttribute` marks an extension:

```C#
    [Extension]
    public class MyExtension : ISomeInterface // Depending on the extension point
    {
        // Your code here
    }
```

The attribute has four named properties, all optional:

* **Path** This is a string that uniquely identifies the extension point to which the extension applies. Generally, the Path will be omitted and NUnit will deduce its value based on the Type. It may be needed in some cases, where classes implement multiple interfaces or inherit other classes that do so. Usually, it won't be needed if you follow the Single Responsibility principle.

* **Description** An optional description of what the extension does.

* **Enabled** A boolean flag indicating whether the extension is enabled. This defaults to true. The setting is used by advanced extensions with functionality that is turned on and off depending on user input.

* **EngineVersion** The minimum engine version supported by this extension. It is suggested that you use this property if your extension only works with higher versioned engines, even if you only use those higher versions. However, the ability to check this property was only added to the engine with version 3.4, so you should avoid installing such extensions at all if you use lower versions of the engine.

####ExtensionPropertyAttribute

Using only the `ExtensionAttribute`, NUnit would have to create instances of every extension in order to ask questions like "What file extensions do you support." This would mean loading many potentially unneeded assemblies.

The `ExtensionPropertyAttribute` avoids the problem. NUnit's own extension for loading NUnit projects is a good example:

```C#
    [Extension]
    [ExtensionProperty("FileExtension", ".nunit")]
    public class NUnitProjectLoader : IProjectLoader
    {
        ...
    }
```

By use of the `ExtensionPropertyAttribute` NUnit is able to avoid loading the extension unless the user asks to run tests in a file of type `.nunit`.

Of course, this means that the extension author must know what properties are suppored by each extension point. For that information, see the individual sections that follow.

##Extension Point Details

In the following sections, we will provide the basic information you need to know about each extension point:
 * The Path that identifies the extension point
 * The Type to be inherited or implemented by your extension.
 * The minimum engine version supporting it
 * Any properties used
 * Sample code

####Project Loaders

 * **Path:** /NUnit/Engine/TypeExtensions/IProjectLoader

 * **Type:** [[IProjectLoader|Project-Loaders]]

 * **Engine Version:** All Versions

 * **Properties:** The **FileExtension** property should be repeated as many times as neede to specify all the file extensions that this project loader is able to support.

 * **Example:**

   ```C#
[Extension]
[ExtensionProperty("FileExtension", ".xxx")]
[ExtensionProperty("FileExtension", ".yyy")]
public class SomeProjectLoader : IProjectLoader
{
    ...
}
   ```

####Result Writers

 * **Path:** /NUnit/Engine/TypeExtensions/IResultWriter

 * **Type:** [[IResultWriter|Result-Writers]]

 * **Engine Version:** All Versions

 * **Properties:** The **Format** property is used to specify the name of the format used on the command-line to indicate this result writer should be used.

 * **Example:**

   ```C#
[Extension]
[ExtensionProperty("Format", "custom")]
public class CustomResultWriterFactory : IResultWriter
{
    ...
}
   ```

####Framework Drivers

 * **Path:** /NUnit/Engine/TypeExtensions/IDriverFactory

 * **Type:** [[IDriverFactory|Framework-Drivers]]

 * **Engine Version:** All Versions

 * **Properties:** None used

 * **Example:**

   ```C#
[Extension]
public class MyOwnFrameworkDriverFactory : IDriverFactory
{
    ...
}
   ```

####Event Listeners

 * **Path:** /NUnit/Engine/TypeExtensions/ITestEventListener

 * **Type:** [[ITestEventListener|Event-Listeners]]

 * **Engine Version:** 3.4 and higher

 * **Properties:** None used

 * **Example:**

   ```C#
[Extension(EngineVersion="3.4")]
public class MyEventListener : ITestEventListener
{
    ...
}
   ```
