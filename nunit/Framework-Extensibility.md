The NUnit Framework is the part of NUnit that is referenced by user tests. It contains the definition of all of NUnit's Attributes, Constraints and Asserts as well as the code that discovers and executes tests. Most extensions to exactly how tests are recognized and how they execute are Framework extensions.

In this documentation, we refer to four different types of Framework extension:

[[Action Attributes]] are designed to better enable composability of test logic by creating attributes that encapsulate specific actions to be taken before or after a test is run.

[[Custom Attributes]] go beyond simple before/after logic and allow creation of new types of tests and suites, new sources of data and modification of the environment in which a test runs as well as its final result.

[[Custom Constraints]] allow the user to define new constraints for use in tests along with the associated fluent syntax that allows them to be used with `Assert.That`.

[[Custom Asserts]] are, for the most part, no longer needed as a result the constraint-based assertion model. However, it is still possible to create them and custom asserts created for NUnit V2 are still useable.
