**AssignableToConstraint** tests that one type is assignable to another

<h4>Constructor</h4>

```C#
AssignableToConstraint( Type )
```

<h4>Syntax</h4>

```C#
Is.AssignableTo( Type )
Is.AssignableTo<T>()
```

<h4>Examples of Use</h4>

```C#
Assert.That( "Hello", Is.AssignableTo(typeof(object)));
Assert.That( 5, Is.Not.AssignableTo(typeof(string)));
```