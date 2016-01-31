**InstanceOfTypeConstraint** tests that an object is of the type supplied or a derived type.

<h4>Constructor</h4>

```C#
InstanceOfTypeConstraint( Type )
```

<h4>Syntax</h4>

```C#
Is.InstanceOf( Type )
Is.InstanceOf<T>()
```

<h4>Examples of Use</h4>

```C#
Assert.That("Hello", Is.InstanceOf(typeof(string)));
Assert.That(5, Is.Not.InstanceOf(typeof(string)));

Assert.That(5, Is.Not.InstanceOf<string>());
```

