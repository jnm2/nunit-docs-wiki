<h2>Page Under Development</h2>

NUnit 2.4 introduced `addins`, which allowed a knowledgeable user to extend the framework by adding new test types, handling events, etc. This approach to extending the framework continued in use through NUnit 2.6.4, the final release of NUnit V2.

In NUnit 3.0, the functions provided by these `addins` are being taken over by the use of [[Custom Attributes]]. This approach is much simpler than the original approach and we think it will promote a great deal of user innovation in extending NUnit. NUnit 3.0 attributes are generally active. That is, they contain code to perform the function they call for rather than simply serving as markers to be interpreted by the runner.
