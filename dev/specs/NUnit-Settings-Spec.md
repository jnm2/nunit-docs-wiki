> **NOTE:** This page is a specification that was used as a starting point for creating the feature in NUnit. It needs to be reviewed and revised in order to accurately reflect what was actually built. If you take it with a grain of salt, it may still be helpful to you as documentation. This notice will be removed when the page is brought up to date.

NUnit makes use of various settings, some built in and others set
by the user. Those set by the user may be set for a single run, for 
a single project or as defaults for all projects.

This page describes the different types of settings and enumerates
existing and planned settings for NUnit 3.0.

##### Built-in Defaults #####

Built-in defaults are part of the code of NUnit itself. Often they
are expressed as a default value for any user settings that are
not found in the NUnitSettings.xml file.

##### User Default Settings #####

User Defaults are contained in the NUnitSettings.xml file and may
be updated using an editor or through the Gui settings dialog.
In the table that follows, the key for the settings file is
given where applicable.

##### Project Settings #####

Project settings are contained in NUnit project file and may
be updated using an editor or through the Gui Project Editor.
In the table that follows, the element or attribute name
is given where applicable. Attributes are specified as
element@attribute.

##### One-time Settings #####

One-time settings for a run may be set using command-line arguments
or - in some cases - by menu selections in the Gui.

### General Settings ###

General settings affect all test runs, whether through the gui, the console runner or a third-party runner.
The notations 2.5 and 3.0 indicate whether the particular setting is available in the respective versions of NUnit.

|  Description       |  Builtin Default  |  User Default  |  Project Setting  |  Console Option  |
|  -----------       |  ---------------  |  ------------  |  -----------------|------------------|
| ApartmentState (1) |        MTA        |      3.0       |         -         |    3.0     |
| ThreadPriority (1) |       Normal      |      3.0       |         -         |    3.0     |
| InternalTraceLevel |        Off        |    2.5, 3.0    |         -         |  2.5, 3.0  |
| ProcessModel       |       Single      |    2.5, 3.0    |      2.5, 3.0     |  2.5, 3.0  |
| DomainUsage        |       Single      |    2.5, 3.0    |      2.5, 3.0     |  2.5, 3.0  |
| ShadowCopy         |        Yes        |    2.5, 3.0    |         -         |   2.5 (2)  |
| ShadowCopyCache    |  %TMP%/nunit20/ShadowCopyCache  |  2.5, 3.0  |  -      |     -      |
| RuntimeFramework   |  See [[Runtime Selection]]      |  -  |   2.5, 3.0     |  2.5, 3.0  |

##### Notes #####

  1. ApartmentState and ThreadPriority are currently set in the configuration for a test assembly or project. This will be replaced by standard user settings and command line options for NUnit 3.0.
  2. The /noshadow command line option will be removed for NUnit 3.0.

### Gui Settings ###

Gui settings determine aspects of the appearance of the Gui runner. These settings are not
controlled on a project or session basis, so only built-in and user default columns are
provided. 

Settings that simply remember the last position of a window or control are 
handled automatically by the gui and are not listed here even though they may be
stored in the NUnitSettings.xml file.

The notations 2.5 and 3.0 indicate whether the particular setting is available in the respective versions of NUnit. Settings planned for 3.0 may change as the new Gui is designed.

| Description                                         |  Builtin Default   |  User Default  |
|-----------------------------------------------------|--------------------|----------------|
| Use the Full or Mini form of the Gui?               |        Full        |  2.5, 3.0  |
| Number of recent projects to list                   |         5          |  2.5, 3.0  |
| Load most recent project at startup?                |        Yes         |  2.5, 3.0  |
| Check that files exist before listing them?         |        Yes         |  2.5, 3.0  |
| Initial tree display on load                        |        Auto        |  2.5, 3.0  |
| Clear results on reload?                            |        Yes         |  2.5, 3.0  |
| Save visual state of projects?                      |        Yes         |  2.5, 3.0  |
| Show check boxes in tree?                           |        No          |  2.5, 3.0  |
| Show each namespace as a test suite?                |        Yes         |  2.5, 3.0  |
| Display the Errors and Failures tab?                |        Yes         |  2.5, 3.0  |
| Enable failure tooltips?                            |        Yes         |  2.5, 3.0  |
| Enable wordwrap in errors display?                  |        Yes         |  2.5, 3.0  |
| Display the Tests Not Run tab?                      |        Yes         |  2.5, 3.0  |
| Standard Gui font                                   |  GenericSansSerif  |  2.5, 3.0  |
| Fixed font used in certain controls                 |  GenericMonospace  |  2.5, 3.0  |
| Display source code from stack trace?               |        No          |  2.5, 3.0  |
| Merge the display of tests in multiple assemblies?  |        No          |  2.5, 3.0  |
| Reload whenever assembly changes?                   |        Yes         |  2.5, 3.0  |
| Rerun tests whenever assembly changes?              |        No          |  2.5, 3.0  |
| Reload before each test run?                        |        No          |  2.5, 3.0  |
| Allow opening Visual Studio files?                  |        No          |  2.5 (1)   |

##### Notes #####

  1. This will no longer be a Gui option but will depend on which plugins are installed. However, the VS Project plugin will be installed by default, since the format is used by multiple IDEs.