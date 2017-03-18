### DRAFT - Not Yet Implemented
Create a makefile that can be used to build and install the framework under Linux. A user can install the framework from source by typing "./configure", "make" and "make install" (as root).

Open source software can be installed usually by using [[Automake|http://www.gnu.org/software/automake/]] and [[Autoconf|http://www.gnu.org/software/autoconf/autoconf.html]] under Linux.

After getting the source code the user can type "./configure" (in order to check the dependencies and configure the Makefile), "make" (for building the NUnit framework) and "make install" (in order to install the framework).

### User Stories

##### An NUnit User working on Linux...

  * gets the source code and builds the NUnit Framework by using the usual sequence "configure", "make" and "sudo make install".
  * gets information about missing dependencies when building the framework from source code.

### Design

A hand-written Makefile calls into the NAnt build file provided by the NUnit Core team. It contains an additional target to install the framework on Linux systems. The locations for the files recommended for Linux systems are described in the [[Mono Application Deployment Guidelines|http://www.mono-project.com/Guidelines:Application_Deployment]].

A configure script is created using [[Autoconf|http://www.gnu.org/software/autoconf/autoconf.html]]. It checks for the required dependencies by calling [[pkg-config|http://linux.die.net/man/1/pkg-config]] and related M4 macros. Required pre-requisites include:

  * NAnt 0.92
  * Mono Runtime (supported versions)
  * Mono SDK

Another makefile will be delivered with the ZIP package containing the binary files. The makefile copies the binaries to the correct locations for Linux systems.

### Outstanding Issues

  * Should we be able to create a tarball with the autotools?
