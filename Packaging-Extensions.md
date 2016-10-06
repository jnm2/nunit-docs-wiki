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

#### Review Milestone Status

1. Check the milestone for the current release to see that there are no open issues. Any issues that are not going to be in this release should be moved to a future milestone. This may be the time to create the next milestone.

2. Make sure that completed issues are marked with the appropriate 'closed' label depending on disposition. The release notes will end up reflecting issues marked closed:done.

3. Check all future open milestones for completed issues. Anything that is completed will be included in this release so change its milestone to the current release.

#### Check Versioning

`AssemblyVersion` and `AssemblyFileVersion` are set in `src\extension\Properties\AssemblyInfo.cs` and should match the version in `build.cake`. These values are normally incremented after a release, but should be checked.

#### Update Copyright Year

The copyright year in all the source files is only updated as they are changed, but the copyright in the `[assembly: AssemblyCopyright("...")]` should be updated to the year of the release.

If necessary, update the year in the general copyright notice `LICENSE.txt`. The `.nuspec` files in solution root contains a copyright line, which should also be updated.

Notices at the top of each source code file are only updated when copyrightable changes are made to the file, not at the time of release.