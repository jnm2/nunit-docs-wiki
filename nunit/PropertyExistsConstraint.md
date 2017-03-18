The `PropertyExistsConstraint` tests for the existence of a named property on an object.

<h4>Constructor</h4>

```C#
PropertyExistsConstraint(string name)
```

<h4>Syntax</h4>

```C#
Has.Property( string )
```

<h4>Examples of Use</h4>

```C#
Assert.That( someObject, Has.Property( "Version" ) );
```

#### See also...
 * [[PropertyConstraint]]

