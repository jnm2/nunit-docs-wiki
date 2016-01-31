**NotConstraint** reverses the effect of another constraint. If the base constraint fails, NotConstraint succeeds. If the base constraint succeeds, NotConstraint fails.

<h4>Constructor</h4>
```C#
NotConstraint()
```

<h4>Syntax</h4>
```C#
Is.Not...
```

<h4>Examples of Use</h4>

```C#
Assert.That( collection, Is.Not.Unique );
Assert.That( 2 + 2, Is.Not.EqualTo(5) );
```
