> **NOTE:** This page is a specification that was used as a starting point for creating the feature in NUnit. It needs to be reviewed and revised in order to accurately reflect what was actually built. If you take it with a grain of salt, it may still be helpful to you as documentation. This notice will be removed when the page is brought up to date.

This specification will try to address how NUnit will be packaged. The first section deals with the logical content of each package we want to make available and how they relate to one another. A second section, to be added at a later point will deal with the format of packages, what software will be used to create them and how they will be distributed.

#### NUnit Package Breakdown

##### Framework

The framework is the part of NUnit that is referenced by user tests. It references no other part of NUnit and no other part references it. It is strictly a library component. It is currently made up of a single assembly, nunit.framework.dll, which is built for various environments. The user selects the version needed and multiple versions may be in use on one machine at the same time.

The framework package needs to be available separately and should not replace older framework versions when installed.

##### Engine

The engine is used by all NUnit runners to execute tests. It may exist on a given machine in multiple versions, in case third-party runners require a particular version.

The engine consists of the nunit.engine, nunit.engine.api and nunit-agent assemblies. The three need to be packaged together but the api also needs to be available separately because runners reference it. Currently the engine uses mono.addins, which will need to be part of the combined package. We are reviewing whether to continue use of mono.addins, however.

Each engine addin will need to be packaged separately. Certain addins will also be bundled in a virtual NUnit package.

The engine may be considered to suggest the framework if the implementation supports that relation.

##### Console Runner

The console depends on the engine API assembly. It requires that some version of the full engine package be available on the system.

##### Gui Runner

The Gui is not yet developed. The package will have the same dependencies as the console runner.

##### Project Editor

The editor reads the project file directly and has no dependencies on other parts of NUnit.

