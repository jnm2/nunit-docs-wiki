> **NOTE:** This page is a specification that was used as a starting point for creating the feature in NUnit. It needs to be reviewed and revised in order to accurately reflect what was actually built. If you take it with a grain of salt, it may still be helpful to you as documentation. This notice will be removed when the page is brought up to date.

####Purpose of the Engine

The NUnit Test Engine is the second layer of the three-layered NUnit architecture. The engine has several important functions:

1. Support discovery, exploration and execution of tests written against various builds and versions of the NUnit framework, NUnitLite and external frameworks, without requiring a reference to any particular assembly.

   1.1 Arrange for executing tests in separate AppDomains, Processes or machines.

   1.2 Handle parallel execution of tests in multiple assemblies (future).

   1.3 Aggregate the results of tests from multiple assemblies.

2. Provide services to the runner (top-level) layer.

   2.1 Access to NUnit settings

   2.2 Info about recently opened files

   2.3 Interpretation of various project formats, resolving them to lists of assemblies

   2.4 Provision of alternative XML output formats beyond the native 3.0 format.

####Engine Variants

The engine is built on various platforms with varying functionality. There are three primary variants:

* The full engine, usually known simply as the `TestEngine`.
* The [[Core Engine]], with minimal functionality.
* The [[Mini-Engine]], tailored to provide configurable levels of functionality.

The following table outlines the functionality of each variant at a high level. It is subject to change.

<table>
<tr><th></th>
    <th colspan=2>Full Engine</th><th>Mini-Engine</th><th colspan=2>Core Engine</th></tr>
<tr><th>Feature</th>
    <th>Console</th><th>Agent</th><th>NETCF<br/>Runner</th><th>VS<br/>Adapter</th><th>Xamarin</th></tr>
<tr><td>Multiple versions of the NUnit framework</td>
    <td>Yes</td><td>Yes</td><td>Yes</td><td>Yes</td><td>Yes</td></tr>
<tr><td>Multiple (different) frameworks</td>
    <td>Yes</td><td>Yes</td><td></td><td></td><td></td></tr>
<tr><td>Separate AppDomain</td>
    <td>Yes</td><td>Yes</td><td>Yes</td><td>Yes</td><td></td></tr>
<tr><td>Separate Process</td>
    <td>Yes</td><td></td><td>Yes</td><td></td><td>(2)</td></tr>
<tr><td>Multiple Assemblies</td>
    <td>Yes</td><td>Yes</td><td>Yes</td><td>(3)</td><td></td></tr>
<tr><td>Multiple AppDomains</td>
    <td>Yes</td><td>Yes</td><td>Yes</td><td>(3)</td><td></td></tr>
<tr><td>Multiple Processes</td>
    <td>Yes</td><td></td><td>Yes</td><td></td><td></td></tr>
<tr><td>NUnit Settings</td>
    <td>Yes</td><td>Yes</td><td></td><td></td><td></td></tr>
<tr><td>NUnit Projects (1)</td>
    <td>Yes</td><td></td><td></td><td></td><td></td></tr>
<tr><td>Visual Studio Projects (1)</td>
    <td>Yes</td><td></td><td></td><td></td><td></td></tr>
<tr><td>NUnit V2 Result File (1)</td>
    <td>Yes</td><td></td><td></td><td></td><td></td></tr>
<tr><td>NUnit V2 Driver (1)</td>
    <td>Yes</td><td>Yes</td><td></td><td>(4)</td><td></td></tr>
<tr><td>User Extensions</td>
    <td>Yes</td><td></td><td></td><td></td><td></td></tr>
</table>

######Notes

1. Features currently implemented as an extension would need to be re-implemented if they are needed in an engine variant that doesn't support extensions. This is feasible, since all these features started life as part of the engine, but it does impact the engine design.

2. TCP based communication to the desktop would be nice to have, but probably post 3.0 since it would also likely involve figuring out how to launch processes on each of the supported device OSs.

3. The VS Adapter can run multiple assemblies, but it only needs to deal with one at a time. It creates a separate AppDomain for each assembly.

4. NUnit Settings are not currently used but might be useful in the adapter, since it runs on the development machine where the settings xml file is located.

####Full Engine

This is the full TestEngine, providing complete functionality. It is used on the developer machine and may control other engines on the same or other machines or on attached devices.

The engine that is initially created by a runner is considered the primary engine. Other engines with which it communicates are considered as secondary engines. The full engine may be used in either the primary or secondary role. As a secondary engine, it is executed by the nunit-agent program.

####Core Engine

The [[Core Engine]] supports minimal functionality and is built as a portable library. It is used in various device environments and is one alternative being considered for use by the Visual Studio Test Adapter.

####Mini-Engine

The [[Mini-Engine]] would support various levels of functionality between the full engine and core engine. We are still evaluating whether to build it. It's primary usage would be under the compact framework and it is also an alternative for the the Visual Studio Test Adapter to use.

