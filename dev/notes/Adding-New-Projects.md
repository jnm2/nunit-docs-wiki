#### Adding to nunit.sln and nunit.linux.sln

The main repository for NUnit code is the **nunit/nunit** repository on GitHub. It contains code for the framework, the test engine and the console runner.

This repo contains two main solution files, **nunit.sln** and **nunit.linux.sln**. The first is used when building on Windows, the second on Linux. New projects added should normally also be added to both solutions, unless they are not supported on one platform or the other.

#### Updating the MsBuild Script

The **NUnit.proj** script is used to build nunit on both platforms under MsBuild or XBuild. It does not refer to the solution files, but builds each project individually. Consequently, code must be added to build any new project.

Normally, it is sufficient to add the new project to one of the four properties, contained in ItemGroups at the end of the file:

<table>
<tr><th>NUnitProjects</th><td>Projects that are part of the full NUnit framework</td></tr>
<tr><th>NUnitLiteProjects</th><td>Projects that are part of the NUnitLite framework</td></tr>
<tr><th>EngineProjects</th><td>Projects that are part of the Engine layer</td></tr>
<tr><th>ConsoleProjects</th><td>Projects that are part ofthe console runner</td></tr>
</table>

If a project is only built on a particular platform, a Condition attribute should be used in its entry.

#### References to Other Projects

The architecture of NUnit uses three distinct layers: framework, engine and runners. Within one layer, use Project References to refer to a different project as needed. References across layers are strictly limited, as follows:

 * Runners may refer to nunit.engine.api, but to no other part of the engine. This is part of the design of NUnit and is intended to allow runners to interface with an installed engine without knowing where it is located.

 * Runners may not refer to the framework at all but should work through the engine.

 * The engine may not refer to any runner or to the framework.

 * The framework may not refer to any runner or to the engine.

 * Tests of the engine and runners refer to the framework project but no other cross-layer references should be used. Currently, the console tests refer directly to the engine in order to simulate certain engine behavior in the tests. We will work to remove this reference and new code should not exploit it without first discussing the need to do so among the developers.

#### Setting the Object Directory

If you are adding a project to the solution that mirrors the source code of one of the other projects (for example, nunit.framework-2.0.csproj and nunit.framework-4.5.csproj compile the same source code in the same directory), then you must edit the project file and manually set a **unique** intermediate output directory. If you do not do this, the results of one build might be copied into the output directory for another version causing hard to track down errors. For example, the .NET 4.5 version of nunit.framework.dll might be copied into the .NET 2.0 output directory.

To do this, you must unload your project from Visual Studio and edit the XML. Add the following line to the end of the first `PropertyGroup` in the project.

```xml
<IntermediateOutputPath>obj\$(Configuration)\net-2.0\</IntermediateOutputPath>
```

Modify the `net-2.0` in the path to a value that is unique for your project. If you have any questions, just look at the other framework projects.