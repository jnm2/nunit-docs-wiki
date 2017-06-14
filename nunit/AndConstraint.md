**AndConstraint** combines two other constraints and succeeds only if they both succeed.

#### Constructor

```C#
AndConstraint(Constraint left, Constraint right)
```

#### Syntax

```C#
<Constraint>.And.<Constraint>
```

#### Examples of Use

```C#
Assert.That(2.3, Is.GreaterThan(2.0).And.LessThan(3.0));
```

#### See also...
 * [[OrConstraint]]
