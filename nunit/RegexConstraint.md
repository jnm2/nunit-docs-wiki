**RegexConstraint** tests that a pattern is matched.

<h4>Constructor</h4>
```C#
RegexConstraint(string pattern)
```

<h4>Syntax</h4>
```C#
Does.Match(string pattern)
Matches(string pattern)
```

<h4>Modifiers</h4>
```C#
...IgnoreCase
```

<h4>Examples of Use</h4>
```C#
string phrase = "Make your tests fail before passing!"

Assert.That( phrase, Does.Match( "Make.*tests.*pass" ) );
Assert.That( phrase, Does.Not.Match( "your.*passing.*tests" ) );
Expect( phrase, Matches( "Make.*pass" ) );
```

<h4>Notes</h4>
1. <b>Matches</b> may appear only in the body of a constraint 
   expression or when the inherited syntax is used.
