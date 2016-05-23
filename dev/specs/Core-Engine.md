The core engine is a non-extensible, minimal engine for use by devices and similar situations where reduced functionality is compensated for by reduced size and simplicity of usage. It supports the complete ITestEngine interface but the implementation of each method or property is limited.

See [[Test Engine]] for a discussion of the other engine variants we are supporting or considering.

####Differences from the Full TestEngine

* Mono.addins is not used, so plugins are not supported.

* Only the direct runner is supported, for use in the same or a separate AppDomain.

* Only the NUnit3FrameworkDriver is supported.

* The only Services supported are the SettingsService and the DomainManager service (but see below).

* A separate nunit.engine.api assembly is not used. Interfaces are defined directly in nunit.core.engine.

* The core engine is intended to be directly referenced by a runner, not created indirectly like the full engine.

####Implementation

We will attempt to implement the core engine as a portable library. Some experimentation is required in order to determine whether this is possible.