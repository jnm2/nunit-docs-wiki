Through the 2.6 series, NUnit was maintained as a single large project.
Development of NUnit 3.0 is being carried out as a set of separate, but
coordinated projects.

The overall NUnit 3.0 platform is called the **NUnit Extended Testing Platform**
and consists of the following projects:

* The **NUnit Framework** holds the Assertions, Constraints
and other types referenced by users in their tests. It also contains the
the low-level code used to actually discover and execute tests.

* **NUnitLite** is a lightweight version of NUnit in a single assembly.
It runs in resource-poor environments and is actually developed as part
of the NUnit Framework project, using a common codebase.

* The **NUnit-Console** program is an updated version of the existing console
runner, designed to work with NUnit 3.0.

* The NUnit **Test Execution Engine** is a new component, which will provide a 
common API to be used by all programs that run NUnit tests. It is actually
currently maintained as a part of the NUnit-Console project, but may be 
split off when its features are stabilized.

* The **NUnit-GUI** project will create a new interactive runner for NUnit 3.0
to replace the old "nunit.exe" program. Work has not yet been started on this project.

* The **NUnit Visual Studio Test Adapter** allows running tests under the Visual
Studio 2012 / 2013 Test Explorer window.

* Other projects will be added as time goes on, including additional interactive
runners, a configuration program and a Visual Studio extension.

