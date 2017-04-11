An EqualConstraint is used to test whether an actual value
is equal to the expected value supplied in its constructor,
optionally within a specified tolerance.

<h4>Constructor</h4>

```C#
EqualConstraint( object expected )
```

<h4>Syntax</h4>

```C#
Is.EqualTo( object expected )
Is.Zero // Equivalent to Is.EqualTo(0)
```

<h4>Modifiers</h4>

```C#
...IgnoreCase
...AsCollection
...NoClip
...WithSameOffset
...Within(object tolerance)
      .Ulps
      .Percent
      .Days
      .Hours
      .Minutes
      .Seconds
      .Milliseconds
      .Ticks
...Using(IEqualityComparer comparer)
...Using(IEqualityComparer<T> comparer)
...Using(IComparer comparer)
...Using<T>(IComparer<T> comparer)
...Using<T>(Comparison<T> comparer)
```

<h4>Comparing Numerics</h4>
Numerics are compared based on their values. Different types
may be compared successfully if their values are equal.
   
Using the <b>Within</b> modifier, numerics may be tested
for equality within a fixed or percent tolerance.

```C#
Assert.That(2 + 2, Is.EqualTo(4.0));
Assert.That(2 + 2 == 4);
Assert.That(2 + 2, Is.Not.EqualTo(5));
Assert.That(2 + 2 != 5);
Assert.That( 5.0, Is.EqualTo( 5 );
Assert.That( 5.5, Is.EqualTo( 5 ).Within(0.075));
Assert.That( 5.5, Is.EqualTo( 5 ).Within(1.5).Percent);
```

<h4>Comparing Floating Point Values</h4>
Values of type float and double are normally compared using a tolerance
specified by the <b>Within</b> modifier. The special values PositiveInfinity, 
NegativeInfinity and NaN compare
as equal to themselves.

Floating-point values may be compared using a tolerance
in "Units in the Last Place" or ULPs. For certain types of numerical work,
this is safer than a fixed tolerance because it automatically compensates
for the added inaccuracy of larger numbers.

```C#
Assert.That( 2.1 + 1.2, Is.EqualTo( 3.3 ).Within( .0005 ));
Assert.That( double.PositiveInfinity, Is.EqualTo( double.PositiveInfinity ));
Assert.That( double.NegativeInfinity, Is.EqualTo( double.NegativeInfinity ));
Assert.That( double.NaN, Is.EqualTo( double.NaN ));
Assert.That( 20000000000000004.0, Is.EqualTo(20000000000000000.0).Within(1).Ulps);
```

<h4>Comparing Strings</h4>

String comparisons normally respect case. The <b>IgnoreCase</b> modifier 
causes the comparison to be case-insensitive. It may also be used when 
comparing arrays or collections of strings.

```C#
Assert.That( "Hello!", Is.Not.EqualTo( "HELLO!" ));
Assert.That( "Hello!", Is.EqualTo( "HELLO!" ).IgnoreCase);

string[] expected = new string[] { "Hello", World" };
string[] actual = new string[] { "HELLO", "world" };
```

#### Comparing DateTimes and TimeSpans

<b>DateTimes</b> and <b>TimeSpans</b> may be compared either with or without
a tolerance. A tolerance is specified using <b>Within</b> with either a 
<b>TimeSpan</b> as an argument or with a numeric value followed by a one of 
the time conversion modifiers: <b>Days</b>, <b>Hours</b>, <b>Minutes</b>,
<b>Seconds</b>, <b>Milliseconds</b> or <b>Ticks</b>.

When comparing <b>DateTimeOffsets</b> you can use the optional <b>WithSameOffset</b>
modifier to check the offset along with the date and time.

```C#
DateTime now = DateTime.Now;
DateTime later = now + TimeSpan.FromHours(1.0);

Assert.That( now, Is.EqualTo(now));
Assert.That( later. Is.EqualTo(now).Within(TimeSpan.FromHours(3.0));
Assert.That( later, Is.EqualTo(now).Within(3).Hours);
```

<h4>Comparing Arrays, Collections and IEnumerables<h4>

Since version 2.2, NUnit has been able to compare two single-dimensioned arrays.
Beginning with version 2.4, multi-dimensioned arrays, nested arrays (arrays of arrays)
and collections may be compared. With version 2.5, any IEnumerable is supported.
Two arrays, collections or IEnumerables are considered equal if they have the
the same dimensions and if each of the corresponding elements is equal.
	
If you want to treat two arrays of different shapes as simple collections 
for purposes of comparison, use the <b>AsCollection</b> modifier, which causes 
the comparison to be made element by element, without regard for the rank or 
dimensions of the array. Note that jagged arrays (arrays of arrays) do not
have a single underlying collection. The modifier would be applied
to each array separately, which has no effect in most cases. 

The `AsCollection` modifier is also useful on classes implementing both `IEnumerable`
and `IEquatable`. Without the modifier, the `IEquatable` implementation is used to
test equality. With the modifier specified, `IEquatable` is ignored and the contents
of the enumeration are compared one by one.

```C#
int[] i3 = new int[] { 1, 2, 3 };
double[] d3 = new double[] { 1.0, 2.0, 3.0 };
int[] iunequal = new int[] { 1, 3, 2 };
Assert.That(i3, Is.EqualTo(d3));
Assert.That(i3, Is.Not.EqualTo(iunequal));

int array2x2 = new int[,] { { 1, 2 } { 3, 4 } };
int array4 = new int[] { 1, 2, 3, 4 };		
Assert.That( array2x2, Is.Not.EqualTo( array4 ));
Assert.That( array2x2, Is.EqualTo( array4 ).AsCollection );
```

<h4>Comparing Dictionaries</h4>

Two dictionaries are considered equal if

<ol>
<li>The list of keys is the same - without regard to ordering.
<li>The values associated with each key are equal.
</ol>

You can use this capability to compare any two objects implementing
<b>IDictionary</b>. Generic and non-generic dictionaries (Hashtables) 
may be successfully compared.

<h4>Comparing DirectoryInfo</h4>

Two DirectoryInfo objects are considered equal if
both have the same path, creation time and last access time.

```C#
Assert.That(new DirectoryInfo(actual), Is.EqualTo(expected));
```

<h4>User-Specified Comparers</h4>

If the default NUnit or .NET behavior for testing equality doesn't
meet your needs, you can supply a comparer of your own through the
<b>Using</b> modifier. When used with <b>EqualConstraint</b>, you
may supply an <b>IEqualityComparer</b>, <b>IEqualityComparer&lt;T&gt;</b>,
<b>IComparer</b>, <b>IComparer&lt;T&gt</b>; or <b>Comparison&lt;T&gt;</b> 
as the argument to <b>Using</b>.

```C#
Assert.That( myObj1, Is.EqualTo( myObj2 ).Using( myComparer ));
```

Prior to NUnit 2.6, only one comparer could be used. If multiple
comparers were specified, all but one was ignored. Beginning with NUnit 2.6,
multiple generic comparers for different types may be specified. NUnit 
will use the appropriate comparer for any two types being compared. As a result,
it is now possible to provide a comparer for an array, a collection type or
a dictionary. The user-provided comparer will be used directly, bypassing the
default NUnit logic for array, collection or dictionary equality.

```C#
class ListOfIntComparer : IEqualityComparer<List<int>>
{
	...
}

var list1 = new List<int>();
var list2 = new List<int>();
var myComparer = new ListOfIntComparer();
...
Assert.That( list1, Is.EqualTo(list2).Using( myComparer ));
```

<h4>Notes</h4>
<ol>
<li><p>When checking the equality of user-defined classes, NUnit first examines each class to determine whether it implements `IEquatable<T>` (unless the `AsCollection` modifier is used). If either object implements the interface for the type of the other object, then that implementation is used in making the comparison. If neither class implements the appropriate interface, NUnit makes use 
    of the <b>Equals</b> override on the expected object. If you neglect to either implement <b>IEquatable&lt;T&gt;</b> or to
	override <b>Equals</b>, you can expect failures comparing non-identical objects. 
	In particular, overriding <b>operator==</b> without overriding <b>Equals</b>
or implementing the interface has no effect.
<li><p>The <b>Within</b> modifier was originally designed for use with floating point
    values only. Beginning with NUnit 2.4, comparisons of <b>DateTime</b> values 
	may use a <b>TimeSpan</b> as a tolerance. Beginning with NUnit 2.4.2, 
	non-float numeric comparisons may also specify a tolerance.
<li><p>Beginning with NUnit 2.4.4, float and double comparisons for which no 
	tolerance is specified use a default, use the value of
	<b>GlobalSettings.DefaultFloatingPointTolerance</b>. If this is not
	set, a tolerance of 0.0d is used.
<li><p>Prior to NUnit 2.2.3, comparison of two NaN values would always fail,
    as specified by IEEE floating point standards. The new behavior, was
	introduced after some discussion becuase it seems more useful in tests. 
	To avoid confusion, consider using <b>Is.NaN</b> where appropriate.
<li><p>When an equality test between two strings fails, the relevant portion of
	of both strings is displayed in the error message, clipping the strings to
	fit the length of the line as needed. Beginning with 2.4.4, this behavior
	may be modified by use of the <b>NoClip</b> modifier on the constraint. In
	addition, the maximum line length may be modified for all tests by setting
	the value of <b>TextMessageWriter.MaximumLineLength</b> in the appropriate
	level of setup.
<li><p>When used with arrays, collections or dictionaries, EqualConstraint 
    operates recursively. Any modifiers are saved and used as they apply to 
	individual items.
<li><p>A user-specified comparer will not be called by <b>EqualConstraint</b>
    if either or both arguments are null. If both are null, the Constraint
	succeeds. If only one is null, it fails.
<li><p>NUnit has special semantics for comparing <b>Streams</b> and
<b>DirectoryInfos</b>. For a <b>Stream</b>, the contents are compared.
For a <b>DirectoryInfo</b>, the first-level directory contents are compared.
</ol>
