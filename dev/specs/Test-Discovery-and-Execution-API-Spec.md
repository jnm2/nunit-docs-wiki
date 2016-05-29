> **NOTE:** This page is a specification that was used as a starting point for creating the feature in NUnit. It needs to be reviewed and revised in order to accurately reflect what was actually built. If you take it with a grain of salt, it may still be helpful to you as documentation. This notice will be removed when the page is brought up to date.

This spec summarizes the three levels of APIs provided by NUnit for discovering and running tests. Note that only one of them - the highest level - is supported for general usage. The others have very specific purposes and should only be used for those purposes.

The three APIs, from highest to lowest level, are:

* **Test Engine API** - for use by any program that needs to discover and execute tests.
* **Engine Driver API** - for use by framework drivers, intended to be loaded by the engine to enable communication with a particular framework.
* **Framework API** - only used by NUnit's own framework driver to communicate with the framework.

![](https://docs.google.com/drawings/d/1eBVjjrWtiqgyIod_ld0rjtyLdeLYzXs_JMGHkhkZaJw/pub?w=361&h=434)

####Test Engine API

The NUnit TestEngine is a separate component, new to NUnit 3.0, which knows how to discover and execute tests. It provides an API for both simple batch execution and more complex interaction as needed by typical Gui test runners. It also provides additional Engine services beyond what the framework provides. This is what we recommend for use by anyone needing to run NUnit tests programatically.

See [[Test Engine API Spec]] for more info.

####Engine Driver API

The NUnit TestEngine uses drivers to communicate with test frameworks. The initial 3.0 releases came with NUnit 3.0 and NUnit 2.x drivers. It is possible to create a driver for running any sort of test framework, supporting any language at all. The driver API is what makes this possible.

The driver API is only intended to be implemented by drivers and is only used by the NUnit engine. See [[Engine Driver API Spec]] for more info.

####NUnit Framework API

This is a primitive API implemented by the NUnit 3 Framework. The NUnitFrameworkDriver in the engine uses this API. The API is a bit complicated to use. Since it needs to support multiple versions of the framework, it uses well-known framework class names, which are constructed via reflection. All results are returned as raw XML. 

This API is not intended for any use except by NUnit itself. See [[Framework API Spec]] for more info.
