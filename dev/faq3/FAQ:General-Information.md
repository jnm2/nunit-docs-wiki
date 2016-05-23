### Who should read this FAQ?

This FAQ is aimed at NUnit developers and contributors, authors of addins and anyone else who needs to build NUnit from source.

Depending on the nature of your interest, different sections of the FAQ and different questions will apply to you.

### How does the NUnit 3.0 project structure differ from earlier versions?

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

### Where can I get the source code for a release of NUnit?

The source code for each release of NUnit is available as a [[download|http://nunit.org/?p=download]], with a name like "NUnit-2.6.2-src.zip." You would normally not want to use a release version of the source when working on bug fixes or features for NUnit, since that source becomes out of date very quickly.
		 
However, you may want to use a release version of the source...

  * To create a debug version of a particular release and step through it.
  * To make your own local changes to NUnit
  * To learn how NUnit works

### Will building from source interfere with my production copy of NUnit?

No. NUnit is capable of existing on a machine in many different builds and versions. However,
you should ensure that you don't use the same version number in your builds as one of the
installed NUnit versions.

### Where is NUnit development hosted?

NUnit development is currently hosted on [[Launchpad|http://launchpad.net/nunit-xtp]] but
we are in the process of moving it to [[GitHub|https://github.com/nunit/]].

GithHub provides an environment that encourages individuals to work on
open source projects with a very low entry barrier. No special permission
is needed to fork any repository and all your changes can be pushed to your fork on GitHub.
GitHub also makes it easy to merge your changes into the main project using Pull Requests.

Since we are anxious to have increased community involvement in NUnit
development, GitHub seems to be an ideal host for us.  See
[[Migration to Github]] for the current status of this ongoing change.

**Note:** *Versions through 2.5.2 were maintained on [[Sourceforge|http://sourceforge.net/projects/nunit]],
where you can still find the code for older releases.*

