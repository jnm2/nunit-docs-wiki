**AndConstraint** combines two other constraints and succeeds only if they both succeed.

<h4>Constructor</h4>

```C#
AndConstraint(Constraint left, Constraint right)
```

<h4>Syntax</h4>

```C#
<Constraint>.And.<Constraint>
```

<h4>Examples of Use</h4>

```C#
Assert.That( 2.3, Is.GreaterThan( 2.0 ).And.LessThan( 3.0 ) );
```

#### See also...
 * [[OrConstraint]]
