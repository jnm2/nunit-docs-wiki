The NUnit Console/Engine currently ships with the following extensions,

* NUnit.Extension.NUnitProjectLoader
* NUnit.Extension.VSProjectLoader
* NUnit.Extension.NUnitV2ResultWriter
* NUnit.Extension.NUnitV2Driver
* NUnit.Extension.TeamCityEventListener

All but the TeamCityEventListener are built and shipped by the NUnit team. These extensions must be built and released before building and releasing the Console/Engine, but only if they are changed and a release is planned. For the 3.5 release, all extensions will be built and released with the console. Future releases of each extension will be on an as-needed basis and the version numbers of the extensions and the console/engine will diverge over time.

####Building an Extension

Begin by getting 