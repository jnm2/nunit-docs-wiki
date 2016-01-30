NUnit isolates test assemblies from its own code and from one another
by use of separate Processes and AppDomains.
   
By default, NUnit loads each test assembly into a separate <b>Process</b>
under the control of the [[NUnit Agent]]
program. This allows NUnit to ensure that each assembly is loaded in the environment
for which it was built. Within the agent process, NUnit's own code runs in the primary   
<b>AppDomain</b> while the tests run in a separate <b>AppDomain</b>.
   
If desired, multiple test assemblies may be loaded into the same process and
even the same domain by use of the <b>-process</b> and <b>-domain</b> command-line
options. See [[Console Command Line]].
