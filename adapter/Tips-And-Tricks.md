> ﻿NOTE:
> As of the 3.0 final release, these registry settings are no longer recognized. Instead, use settings in the `.runsettings` file. 


## NUnit 3.x

### VS Test .Runsettings configuration
Certain NUnit Test Adapter settings are configurable using a .runsettings file. 
The following options are available:

|Key|Type|Options| Default|
|---|----|-------|--------------|
|InternalTraceLevel| string |  Off, Error, Warning, Info, Verbose,  Debug| Nothing => Off|
|NumberOfTestWorkers| int | nr of workers | -1|
|ShadowCopyFiles| bool |True, False | False|
|Verbosity| int | 0-5 ? | 0|
|UseVsKeepEngineRunning| bool | True, False| False|
|BasePath| string | path| ?|
|PrivateBinPath | string| directory1;directory2;etc |?|
|RandomSeed| int | seed integer| random|

### Example implementation
See https://github.com/nunit/nunit3-vs-adapter/blob/8a9b8a38b7f808a4a78598542ddaf557950c6790/demo/demo.runsettings

### NUnit .runsettings implementation

https://github.com/nunit/nunit3-vs-adapter/blob/master/src/NUnitTestAdapter/AdapterSettings.cs#L143


### Details

#### InternalTraceLevel
This setting is a diagnostic setting forwarded to NUnit, and not used by the adapter itself.  For further information see the [NUnit Tracelevel documentation](https://github.com/nunit/docs/wiki/Internal-Trace)

#### NumberOfTestWorkers
This  setting is sent to NUnit to determine how  [parallelization](https://github.com/nunit/docs/wiki/Parallelizable-Attribute) should be performed.  

#### ShadowCopyFiles
This setting is sent to NUnit to enable/disable shadow-copying. 

#### Verbosity
This controls the outputs from the adapter to the Visual Studio Output/Tests window.
A higher number includes the information from the lower numbers.
It now has the following actual levels:

0 : Default, lowest verbosity

1-3: Some more information from setting are output (in particular regarding parallelization)

4: Outputs the values from the  runsettings it has discovered.

5: Outputs all debug statements in the adapter



#### UseVsKeepEngineRunning
This setting is used by the adapter to signal to the VSTest.Execution engine to keep running after the tests have finished running.  This can speed up execution of subsequent test runs, as the execution engine already is loaded, but running the risks of either holding onto test assemblies and having some tests not properly cleaned out.   The settings is the same as using the Visual Studio  Test/Test Settings/Keep Test Execution Engine running. 




## NUnit 2.x


### Registry Settings 

Certain settings in the registry affect how the adapter runs. All these settings are added by using RegEdit under the key **HKCU\Software\nunit.org\VSAdapter**.

#### ShadowCopy

By default NUnit no longer uses shadowcopy. If this causes an issue for you shadowcopy can be enabled by setting the DWORD value UseShadowCopy to 1.   
  
#### KeepEngineRunning

By default the NUnit adapter will "Kill" the Visual Studio Test Execution engine after each run. Visual Studio 2013 and later has a new setting under its top menu, **Test | Test Settings | Keep Test Execution Engine Running**. The adapter normally ignores this setting.

In some cases it can be useful to have the engine running, e.g. during debugging of the adapter itself. You can then set the adapter to follow the VS setting by setting the DWORD value UseVsKeepEngineRunning to 1.

#### Verbosity

Normally the adapter reports exceptions using a short format, consisting of the message only. You can change it to report a verbose format that includes the stack trace, by setting a the DWORD value Verbosity to 1.




