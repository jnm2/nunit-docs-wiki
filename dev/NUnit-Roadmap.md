> **NOTE:** This page is completely out of date. We need to decide whether to continue maintaining it or remove it.

This page is a first draft of a roadmap taking us to an NUnit 3.0 release. 

####NUnit 3.0 Initial Alpha Release

* All NUnit 2.6 features being removed should be removed before the first alpha
* All NUnit 2.6 features that are NOT being removed should be in place
* All outstanding bugs marked as "Review" or "Confirm" should be either closed or assigned a priority
* All outstanding Critical and high priority bugs should be resolved
* Framework, Engine and Console included
* Framework and Engine Apis reasonably stable
* Combined zip file for full installation
* NuGet package for full and nunitlite frameworks

#####Platform Support

* .NET 4.5, 4.0, 3.5 and 2.0 and corresponding Mono platforms
* Silverlight 5.0

#####Specific Features

* Implement ActionAttributes (#112)
* Implement Changes to File, Directory and Path Assertions (#111)
* Standardize commandline options for nunitlite runner (#13)

####NUnit 3.0 Final Release

* All outstanding Critical, High and Normal priority bugs should be resolved.
* Framework, Engine, Console and Gui included
* Framework, Driver and Engine Apis stable
* Combined zip file and Msi installer for full installation
* VSix and NuGet packages for 3.0-based test adapter
* NuGet package for full and nunitlite frameworks

#####Platform Support

* .NET 4.5, 4.0, 3.5 and 2.0 and corresponding Mono platforms
* Silverlight 5.0, possibly 4.0
* Windows Phone 8.0 and 8.1
* Possibly, .NET CF 3.9 (1)

#####Specific Features

* Parallel Test Execution within assemblies (#66)
* Run test assemblies in parallel (Console#7)
* NUnit-Console should support incremental output under TeamCity (Console#7)
* Full async support (review outstanding issues to define this more clearly)
* Included driver for NUnit 2.x tests

####Notes

1. Compact framework is not a high priority, but 3.9 is listed since we are removing the existing 2.0 and 3.5 support. If we can simply substitute 3.9 for 3.5 without significant changes, as advertised, then we will retain the code for it.

####Outstanding Issues

* Timing for additional platforms we want to support.
* Other features to be added