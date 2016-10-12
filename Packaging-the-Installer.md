Before packaging the installer, you must first package and release the Console and Engine. See [[Packaging the Console and Engine]]

### Prepare the Release

1. Get latest from master
2. Delete the `image` and `distribution` directories
3. Check the `version` and `displayVersion` in `build.cake`
4. Package the release, `.\build.ps1` or `.\build.cmd`
5. Check the `distribution` directory for `NUnit.{VERSION}.msi` and `NUnit.{VERSION}.zip`

### Test the Release

#### Test the Installer

1. Install `NUnit.{VERSION}.msi`
2. Ensure it installs correctly
3. Check that the extensions included in `build.cake` are installed
4. Run unit tests using the install
5. Ensure the extensions work by running NUnit 2 tests and by creating NUnit 2 test results
6. Check the version in the `nunit3-console.exe` output headers when running tests.

#### Test the ZIP File

1. Unzip `NUnit.{VERSION}.zip`
2. Check that the extensions included in `build.cake` are installed
3. Run unit tests using the install
4. Ensure the extensions work by running NUnit 2 tests and by creating NUnit 2 test results
5. Check the version in the `nunit3-console.exe` output headers when running tests.

#### Archiving the Release

Packages are archived on nunit.org in the downloads directory. Add the MSI and ZIP to the existing downloads/nunit/v3 for the Console/Engine release.

#### Publishing the Release

1. Log onto Github and go to the main nunit-console repository at https://github.com/nunit/nunit-console.
2. Go to the releases tab and edit the existing Console release
3. Add the MSI and ZIP files to the release
