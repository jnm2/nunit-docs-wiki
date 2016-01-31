**EndsWithConstraint** tests for an ending string.

<h4>Constructor</h4>
```C#
EndsWithConstraint(string expected)
```

<h4>Syntax</h4>
```C#
Does.EndWith(string expected)
EndsWith(string expected)
```

<h4>Modifiers</h4>
```C#
...IgnoreCase
```

<h4>Examples of Use</h4>
```C#
string phrase = "Make your tests fail before passing!"

Assert.That( phrase, Does.EndWith( "!" ) );
Assert.That( phrase, Does.EndWith( "PASSING!" ).IgnoreCase );
Expect( phrase, EndsWith( "!" ) );
```

<h4>Notes</h4>
1. <b>EndsWith</b> may appear only in the body of a constraint 
   expression or when the inherited syntax is used.

