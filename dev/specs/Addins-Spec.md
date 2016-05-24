> **NOTE:** This page is a specification that was used as a starting point for creating the feature in NUnit. It needs to be reviewed and revised in order to accurately reflect what was actually built. If you take it with a grain of salt, it may still be helpful to you as documentation. This notice will be removed when the page is brought up to date.

The NUnit 2.x framework was extensible through the use of NUnit addins. As originally envisioned, NUnit 3.0 was planned to replace our own addin implementation by using Mono.Addins. We expected to support addins for runners, the engine and the framework. See the [[Original Architectural Overview Document | NUnit-3.0-Architecture-(2009)]] for details.

As we worked on NUnit 3.0, we determined that extensibility in the framework layer was better handled by use of custom attributes, as described by the specification [[Addin Replacement in the Framework]]. Consequently, we are supporting addins only in the Engine and Runner layers of NUnit 3.0.

This document describes how we expect to use Mono.Addins but doesn't go into all the details of how they work. That information is available from the Mono.Addins documentation.

####Use of XML Manifests

Mono.Addins allows you to specify extension points and extensions either by use of attributes or through an XML manifest. For NUnit, we will use XML manifests, which are preferred for the following reasons:

1. Some addin features are only available through the use of manifests.

2. Use of an XML file centralizes information about our extension points and addins in one place.

3. By using an XML file, only the engine and any runners that support addins will need to reference Mono.Addins. If attributes were used, then the addins themselves would need to reference the assembly.

User-created addins may use XML manifests or attributes, at the discretion of the programmer.

In general, our manifests will be embedded as resources in the appropriate assemblies. Use of external an external manifest (copied alongside the assembly) is also possible, when it is necessary to exclude any assemblies from being scanned, but we will seek to avoid that necessity by how we organize our directories.

####Extension Roots

Mono.Addins considers both host assemblies and extensions to be 'addins.' Host addins are called 'roots.' Since we are supporting addins for the engine and for our runners, there will be three roots for our extension point trees:

  * NUnit.Gui -- extensions to the (future) GUI.

  * NUnit.Console -- extensions to the console runner.

  * NUnit.Engine -- extensions to the engine itself.

Since we don't yet have a GUI runner, that will not be covered here.

####Console Extension Points

So far, we have not identified extensions needed for the console. Two possible areas for consideration are:

  * NUnit.Console.Options -- specification of additional console options to be supported

  * NUnit.Console.Reports -- specification of additional console reporting output

We'll look into this further as development proceeds.

####Engine Extension Points

Most design work on extensibility so far has ended up focusing on the engine. This is natural, since any functionality that will be needed by both the console and the gui tends to migrate to the engine. The following extension points are currently implemented:

  * NUnit.Engine.Drivers -- drivers used to run certain kinds of tests, e.g. the V2 driver.

  * NUnit.Engine.ProjectLoaders -- loaders for various project formats, e.g.: the VS project loader.

  * NUnit.Engine.OutputWriters -- addins that create output files form the result XML in a particular format, e.g.: the V2 result writer.

However, it's possible that we may want to use addins more extensively, making the engine entirely based on addins. In that case, we may want to consider making all services and runners into (potential) addins.

####Implementation of Mono.Addins

Since Mono.Addins is built for .NET 4.0 and our engine must run under .NET 2.0 and higher, we use a modified build of Mono.Addins in conjunction with NUnit.
