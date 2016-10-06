The NUnit Console/Engine currently ships with the following extensions,

* NUnit.Extension.NUnitProjectLoader
* NUnit.Extension.VSProjectLoader
* NUnit.Extension.NUnitV2ResultWriter
* NUnit.Extension.NUnitV2Driver
* NUnit.Extension.TeamCityEventListener

All but the TeamCityEventListener are built and shipped by the NUnit team. These extensions must be built and released before building and releasing the Console/Engine, but only if they are changed and a release is planned. For the 3.5 release, all extensions will be built and released with the console. Future releases of each extension will be on an as-needed basis and the version numbers of the extensions and the console/engine will diverge over time.

#### Create a Release Branch

All work on releases should be done on a branch.

1. Fetch and pull latest from master
2. Create a branch in the form release/3.5.0
3. As you make the changes below, push the branch to GitHub and create a Pull Request to allow other team members to review your changes.
4. **Do not merge this branch/PR**, we will create a separate PR to merge the changes back into master.

#### Make Sure it Works!

1. Close all instances of Visual Studio or other IDE to ensure that no changes are left unsaved.

2. Do a clean build and run all the tests on Windows. You may use the command below or three separate commands if preferred. If you encounter errors at any stage, you're not actually ready to release!

      `build.cmd -Target=Clean`
      `build.cmd -Target=Test`

3. Repeat the build on a Linux system, if available. If this is not possible, be sure to scrutinize the results from the Travis CI build carefully. On Linux, you may use the command

      `./build -Target=Test`

4. Make sure that the most recent commits of master passed all tests in the CI builds. Check the builds on both Travis and Appveyor.