**AssignableFromConstraint** tests that one type is assignable from another

<h4>Constructor</h4>

```C#
AssignableFromConstraint( Type )
```

<h4>Syntax</h4>

```C#
Is.AssignableFrom( Type )
Is.AssignableFrom<T>()
```

<h4>Examples of Use</h4>

```C#
Assert.That( "Hello", Is.AssignableFrom(typeof(string)));
Assert.That( 5, Is.Not.AssignableFrom(typeof(string)));
```

