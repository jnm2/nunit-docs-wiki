Introduction
------------
There are two purposes for building the adapter, one is for creating the packages for a  release - which is what this page is about, the other is for creating whatever you need for debugging or testing purposes.  For the latter, see [How to build and debug the adapter]

The procedure described here is for those people who need to release a new version of the adapter.

Preparing the source code
-------------------------

#### Update to the latest version of NUnit

This may not be necessary for all releases. However, if the NUnit version used by the adapter is being updated, it is important to do it correctly.

* The NUnit3TestAdapter, NUnit3TestAdapterInstall and NUnit3TestAdapterTests projects should all reference the same version of NUnit Core Engine package, normally the most recent.

* The NUnit3TestAdapterTests and NUnitTestDemo projects should reference the same version of the NUnit framework package, normally the most recent. Note that this is currently the same version as the core engine package, but this may not continue to be the case if the frequency of release of the two packages differs.

#### Versioning
The version numbers follow the basic principles of [semantic versioning]. 
(The fourth number is used for debug versions under development, and will always be 0 for release versions.)

The version numbers have to be edited in the following files, and should match:

* **Assemblyinfo.cs**,  found in the NUnitTestAdapter project
-- change both file and assembly version number
* **source.extensions.vsixmanifest**, found under the NUnitTestAdapterInstall project
-- change Version tag
* **nunit-vs-adapter.build**, found under the Solution Items folder. -- change the version number, but only use the three first digits.
* **license.rtf**, found under the NUnit3TestAdapterInstall project.  If the major/minor number has changed, update that here, 2nd line. If year is changed, update copyright years accordingly. 


Build
-----
Build a release version, AnyCPU. Be sure to use the `Rebuild Solution` menu item in VS. Otherwise, the `.vsix` file may not be regenerated.


Packaging
------

Use NAnt and use the package target
```
NAnt package
```
Run this from the solution root folder

The resulting files can be found in the "package" folder:

  * **NUnit3TestAdapter-[VERSION].vsix**  This is the extension for Visual Studio, which is uploaded to the [Visual Studio Gallery]. 

  * **NUnit3TestAdapter-[VERSION].zip**  This is a zipped package for use with TFS Server Builds when you don't use the NuGet package in your solution. See  [this blog] for more information. 

  * **NUnit3TestAdapter-[VERSION].nupkg** This is the NuGet package, which is uploaded to [Nuget for the adapter]

####Publishing the Release

1. Create a release on GitHub. Few people use this directly, but it is the benchmark release and provides an archive of all past releases, so we do this first. Github will automatically create zip and tar files containing the source. In addition, upload all four packages created above as a part of the release.

2. Upload the vsix package to the [Visual Studio Gallery] using the NUnitDeveloper account. If you don't have access to that account, ask one of the committers with access to do the upload for you.

3. Upload the nuget package to nuget.org. You use your own account for this but you must have been pre-authorized in order for it to work. If you are not authorized, ask a committer with access to do it for you.

4. Update the documentation pages in the wiki as needed. Be sure to update the Release Notes page. In order to perform the update quickly after publishing the packages, you may want to clone the wiki repository and prepare the update in advance.

5. Publicize the release, first announcing it on the nunit-developer and nunit-discuss lists and then more widely as appropriate. [We should develop a list of places.]

#####Note:
  * Publishing the release requires access to various online accounts, which are mentioned above. For obvious reasons, the passwords are not provided. Contact Charlie or Terje if you need this access.

Prerequisites
-----
1. **Visual Studio 2013**
You need Visual Studio 2013.  We use the ultimate edition, but it should be enough with the premium edition.  (I will probably work with both the Pro or the Express editions too, but we haven't tried them).  The latest 1.1 version is built using Update 2 RC. 

1. **Visual Studio 2013 SDK**  
You need this to work with the vsix.  Download from <http://www.microsoft.com/en-us/download/details.aspx?id=40758>

1. **NAnt**
Download from <http://nant.sourceforge.net/>.  We use the 0.92 version.

1. **Nuget**
You need the nuget.exe in your path.  Download the exe from <http://nuget.codeplex.com/downloads/get/784779>.  We use the 2.8 version

1. **VS2012 Testplatform object model**
You need to have this around, the adapter and the testproject refers to this.  The easist way to get it, is to have VS2012 installed and get it from there. 
It is located at a location similar to "C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\CommonExtensions\Microsoft\TestWindow" and is named Microsoft.VisualStudio.TestPlatform.ObjectModel.dll.
You might need to fix up these references if the locations don't match what has been used.






[semantic versioning]:http://semver.org/
[Visual Studio Gallery]:https://visualstudiogallery.msdn.microsoft.com/0da0f6bd-9bb6-4ae3-87a8-537788622f2d
[Nuget for the adapter]:http://www.nuget.org/packages/NUnitTestAdapter/
[Nuget for the adapter with framework]:http://www.nuget.org/packages/NUnitTestAdapter.WithFramework/
[nunit.org repository]:http://github.com/nunit/nunit.org