**OrConstraint** combines two other constraints and succeeds if either of them succeeds.

<h4>Constructor</h4>
```C#
OrConstraint(Constraint left, Constraint right)
```

<h4>Syntax</h4>
```C#
<Constraint>.Or.<Constraint>
```

<h4>Examples of Use</h4>

```C#
Assert.That( 3, Is.LessThan( 5 ).Or.GreaterThan( 10 ) ); 
```

####See also...
 * [[AndConstraint]]
