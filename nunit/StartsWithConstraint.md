**StartsWithConstraint** tests for an initial string.

<h4>Constructor</h4>

```C#
StartsWithConstraint(string expected)
```

<h4>Syntax</h4>

```C#
Does.StartWith(string expected)
StartsWith(string expected)
```

<h4>Modifiers</h4>

```C#
...IgnoreCase
```

<h4>Examples of Use</h4>

```C#
string phrase = "Make your tests fail before passing!"

Assert.That( phrase, Does.StartWith( "Make" ) );
Assert.That( phrase, Does.Not.StartWith( "Break" ) );
Expect( phrase, StartsWith( "Make" ) );
```

<h4>Notes</h4>

1. **StartsWith** may appear only in the body of a constraint 
   expression or when the inherited syntax is used.


