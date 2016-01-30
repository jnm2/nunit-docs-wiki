**Assert.IsNotAssignableFrom** succeeds if the object provided may not be assigned a value of the expected type.

```C#			
Assert.IsNotAssignableFrom( Type expected, object actual );
Assert.IsNotAssignableFrom( Type expected, object actual, 
                            string message, params object[] parms );
Assert.IsNotAssignableFrom<T>( object actual );
Assert.IsNotAssignableFrom<T>( object actual, 
                               string message, params object[] parms );
```

<h4>See also...</h4>
 * [[Type Constraints]]

