**Assert.IsAssignableFrom** succeeds if the object provided may be assigned a value of the expected type.

```C#
Assert.IsAssignableFrom( Type expected, object actual );
Assert.IsAssignableFrom( Type expected, object actual, 
                         string message, params object[] parms );
Assert.IsAssignableFrom<T>( object actual );
Assert.IsAssignableFrom<T>( object actual, 
                            string message, params object[] parms );
```

<h4>See also...</h4>
 * [[Type Constraints]]
