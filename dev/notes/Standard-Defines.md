NUnit uses compiler constants in order to support multiple distributions 
from a single source tree. For convenience, this page categorizes them 
according to their purpose.

**NOTE:** This document refers to NUnit 3.0. Earlier versions used different defines.

### Component Being Built

We identify the component being built for two reasons:

1. To permit conditional inclusion of code for common source shared across components.

2. To distinguish the features supported in different framework builds.

##### NUNIT_CONSOLE
Indicates that we are building the NUnit console runner.

##### NUNIT_ENGINE
Indicates that we are building the NUnit engine.

##### NUNIT_FRAMEWORK
Indicates that we are building the full NUnitFramework.

##### NUNITLITE
Indicates that we are building the NUnitLite runner.

##### ULTRALITE
Reserved for future use.

### Target Runtime

These constants specify the runtime version that is being targeted
by a build. Note that it does **not** refer to the sdk version being
used to create the build, which may be the same or a higher version.

##### NET_2_0
Indicates that the build targets .NET 2.0.

##### NET_3_5
Indicates that the build targets .NET 3.5.

##### NET_4_0
Indicates that the build targets .NET 4.0.

##### NET_4_5
Indicates that the build targets .NET 4.0.

##### NETCF
Indicates that the build targets the compact framework.

##### NETCF_3_5
Indicates that the build targets version 3.5 of the compact framework.

##### NETCF_3_9
Indicates that the build targets version 3.9 of the compact framework.

##### SILVERLIGHT
Indicates that the build targets SilverLight.

##### SL_5_0
Indicates that the build targets SilverLight 5.0.

##### PORTABLE
Indicates that this is a portable class library build.

### Features

##### PARALLEL
Indicates that this build should include parallel execution features.
**Note:** Simply defining this will not provide parallel execution
in platforms that don't support it.

### Vendor

These constants distinguish Microsoft .NET from Mono. They are used 
only in development, in order to temporarily include or exclude code 
which won't compile or causes other problems. Final builds should not 
use these constants.

##### MSNET
Indicates a Microsoft .NET build.

##### MONO
Indicates a Mono build.
