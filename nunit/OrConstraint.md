**OrConstraint** combines two other constraints and succeeds if either of them succeeds.

#### Constructor

```C#
OrConstraint(Constraint left, Constraint right)
```

#### Syntax

```C#
<Constraint>.Or.<Constraint>
```

#### Examples of Use

```C#
Assert.That(3, Is.LessThan(5).Or.GreaterThan(10));
```

#### See also...
 * [[AndConstraint]]
