The constraint-based Assert model uses a single method of the Assert class
for all assertions. The logic necessary to carry out each assertion is
embedded in the constraint object passed as the second parameter to that
method.
   
Here's a very simple assert using the constraint model:

```C#
      Assert.That( myString, Is.EqualTo("Hello") );
```

The second argument in this assertion uses one of NUnit's <b>syntax helpers</b>
to create an <b>EqualConstraint</b>. The same assertion could also be made in this form:

```C#
      Assert.That( myString, new EqualConstraint("Hello") );
```

Using this model, all assertions are made using one of the forms of the
`Assert.That()` method, which has a number of overloads...
   
```C#
Assert.That( bool condition );
Assert.That( bool condition, string message, params object[] parms );

Assert.That( Func<bool> condition );
Assert.That( Func<bool> condition, string message, params object[] parms );              
			 
Assert.That<TActual>( 
    ActualValueDelegate<TActual> del, IResolveConstraint constraint )
Assert.That<TActual>( 
    ActualValueDelegate<TActual> del, IResolveConstraint constraint,
    string message, object[] parms )
             
Assert.That<TActual>( TActual actual, IResolveConstraint constraint )
Assert.That<TActual>( TActual actual, IResolveConstraint constraint,
    string message, params object[] parms )
			 
Assert.That( TestDelegate del, IResolveConstraint constraint );
```

The overloads that take a bool work exactly like Assert.IsTrue.
   
For overloads taking a constraint, the argument must be a object implementing 
the <b>IResolveConstraint</b> interface, which supports performing a test
on an actual value and generating appropriate messages. This interface
is described in more detail under [[Custom Constraints]].
   
NUnit provides a number of constraint classes similar to the <b>EqualConstraint</b>
used in the example above. Generally, these classes may be used directly or
through a syntax helper. The valid forms are described on the pages related to
each constraint.
   
### See also...
 * [[Classic Model]]
   
