**ExactTypeConstraint** tests that an object is an exact Type.

<h4>Constructor</h4>

```C#
ExactTypeConstraint( Type )
```

<h4>Syntax</h4>

```C#
Is.TypeOf( Type )
Is.TypeOf<T>()
```

<h4>Examples of Use</h4>

```C#
Assert.That("Hello", Is.TypeOf(typeof(string)));
Assert.That("Hello", Is.Not.TypeOf(typeof(int)));

Assert.That("World", Is.TypeOf<string>();
```

