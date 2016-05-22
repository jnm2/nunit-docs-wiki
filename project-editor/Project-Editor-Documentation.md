## Project Editor

The NUnit Project editor is a graphical interface for editing [[NUnit Test Projects]]. The editor provides two main views of the project: a property-oriented view, and an xml view, which allows direct editing of the .nunit file.

## Property View

This view consists of a common area and two tabs, as seen in the image below.

![Screenshot of Property View](project-editor/images/generalTab.jpg)

### Common Area

The common area of the Project Editor contains information pertaining to the project as a whole. Information that applies to a particular configuration is displayed in the General and Assemblies tabs.

#### Project Path

This label shows the full path to the project file. In the case of a wrapper project, the path is set to the same directory as the assembly that was initially opened.

#### Application Base

This TextBox allows the user to change the project AppBase, which defaults to the directory of the project file. The button to the right of the TextBox allows the user to browse and select a directory.

#### Process Model

This dropdown list allows you to specify how operating system processes are used in loading and running the tests in this project. Four settings are defined:

*   The **Default** setting refers to the option selected by the user on the Assembly Isolation page of the NUnit Settings Dialog.
*   **Single** means that tests are run in a test domain in the same process as NUnit. This is the way previous versions of NUnit ran tests.
*   **Separate** means that all the tests are run in a separate process that NUnit creates.
*   **Multiple** means that NUnit will create a separate process for each test assembly in the project and run its tests there.

#### Domain Usage

This dropdown list allows you to specify how tests are loaded into AppDomains by NUnit. Three settings are defined:

*   The **Default** setting refers to the option selected by the user on the Assembly Isolation page of the NUnit Settings Dialog.
*   **Single** means that all tests will run in a single test domain created by NUnit.
*   **Multiple** means that each test assembly is loaded into a separate AppDomain. This setting is not available when Multiple processes are selected in the Process Model dropdown.

#### Configuration

This dropdown list allows you to select the particular configuration within a project that is displayed in the bottom part of the dialog.

#### Edit Configs...

This button opens the [[Configuration Editor]], which allows you to add, delete or rename configs and set the active configuration.

### General Tab

The General tab allows setting a number of options pertaining to the selected configuration, all of which will be stored in the NUnit project file as attributes of the `<config>` xml node.

#### Runtime

This dropdown allows you to select a particular runtime framework to be used for loading and running tests under the current configuration. Currently, only Microsoft .NET and Mono are supported. If **Any** is selected, the tests will be run under the same runtime that NUnit itself is currently using.

#### Version

This ComboBox allows you to select the particular version of the runtime framework to be used for loading and running tests under the current configuration. The dropdown list contains entries for

*   Default
*   1.0
*   1.1
*   2.0
*   4.0

If you select "Default" the assemblies in the project are examined to determine the version that is required. See [[Runtime Selection]] for more information on how NUnit selects the version to be used.

In special cases, you may wish to enter a version number that is not listed in the list box. You may specify the version using two, three or four components. The version you provide will be saved as you enter it. Leaving the text box blank is equivalent to selecting "Default."

**Note:** Running tests under a different runtime or version from the one that NUnit is currently using will force them to run in a separate process.

**Note:** To conform with normal usage, specifying Mono as the runtime with "1.0" as the version results in use of the Mono 1.0 profile, equating to version 1.1.4322.

#### ApplicationBase

The ApplicationBase defaults to the directory containing the project file.

#### Configuration File Name

The configuration file defaults to the name of the test project with the extension changed from .nunit to .config. The user may substitute another name.

#### PrivateBinPath

By default, the PrivateBinPath is generated from the assembly locations specified on the Assemblies Tab. For those applications requiring a different level of control, it may be specified manually or using this editor or placed in the configuration file.

### Assemblies Tab

The assemblies tab contains the list of assemblies that form part of this test project.

Note: Although the dialog shows the location of assemblies as absolute paths, they are always persisted in the NUnit project file as paths relative to the application base. This allows moving projects as a whole to a different directory location.

![Screenshot of Assemblies Tab](project-editor/images/assembliesTab.jpg)

#### Add

Opens a dialog allowing adding an assembly to this configuration. If Visual Studio support is enabled, you may also select and add a VS project.

#### Remove

After confirmation, removes the selected assembly from this configuration.

#### Assembly Path

This text box displays the full path to the selected assembly. You may edit the contents to change the path to the assembly.

## XML View

This view simply displays the XML from the project file, as seen here. You may edit the XML directly.

![Screenshot of XML View](project-editor/images/xmlView.jpg)

**Note:** The XML editor is somewhat primitive. Errors in XML formatting are caught and an error message displayed. However, the values of attributes are not validated as they are in the property-based view and it is possible to create a project file, which NUnit is unable to load. Improvements, including intellisense and better error handling, are planned in future versions of the Project Editor.