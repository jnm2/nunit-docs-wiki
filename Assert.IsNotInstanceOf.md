**Assert.IsNotInstanceOf** succeeds if the object provided as an actual value is not an instance of the expected type.

```C#
Assert.IsNotInstanceOf( Type expected, object actual );
Assert.IsNotInstanceOf( Type expected, object actual, 
                         string message, params object[] parms );
Assert.IsNotInstanceOf<T>( object actual );
Assert.IsNotInstanceOf<T>( object actual, 
                        string message, params object[] parms );			
```

<h4>See also...</h4>
 * [[Type Constraints]]
