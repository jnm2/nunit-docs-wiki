**SubstringConstraint** tests for a substring.

<h4>Constructor</h4>
```C#
SubstringConstraint(string expected)
```

<h4>Syntax</h4>
```C#
Does.Contain(string expected)
```

<h4>Modifiers</h4>
```C#
...IgnoreCase
```

<h4>Examples of Use</h4>
```C#
string phrase = "Make your tests fail before passing!"

Assert.That( phrase, Does.Contain( "tests fail" ) );
Assert.That( phrase, Does.Not.Contain( "tests pass" ) );
Assert.That( phrase, Does.Contain( "make" ).IgnoreCase );
```

