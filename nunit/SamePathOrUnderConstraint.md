**SamePathOrUnderConstraint** tests that one path is equivalent to another path or that it is under it.

<h4>Constructor</h4>

```C#
SamePathOrUnderConstraint( string expectedPath )
```

<h4>Syntax</h4>

```C#
Is.SamePathOrUnder( string expectedPath )
```

<h4>Modifiers</h4>

```C#
...IgnoreCase
...RespectCase
```

<h4>Examples of Use</h4>

```C#
Assert.That( "/folder1/./junk/../folder2", 
	Is.SamePathOrUnder( "/folder1/folder2" ) );
Assert.That( "/folder1/junk/../folder2/./folder3",
	Is.SamePathOrUnder( "/folder1/folder2" ) );
Assert.That( "/folder1/junk/folder2/folder3",
	Is.Not.SamePathOrUnder( "/folder1/folder2" ) );

Assert.That( @"C:\folder1\folder2\folder3",
	Is.SamePathOrUnder( @"C:\Folder1\Folder2" ).IgnoreCase );
Assert.That( "/folder1/folder2/folder3",
	Is.Not.SamePathOrUnder( "/Folder1/Folder2" ).RespectCase );
```

#### Notes:

1. Path constraints perform tests on paths, without reference to any
actual files or directories. This allows testing paths that are
created by an application for reference or later use, without 
any effect on the environment.
   
2. Path constraints are intended to work across multiple file systems,
and convert paths to a canonical form before comparing them. 

3. It is usually not necessary to know the file system of the paths
in order to compare them. Where necessary, the programmer may
use the <b>IgnoreCase</b> and <b>RespectCase</b> modifiers to provide 
behavior other than the system default.
      
#### See also...
 * [[SamePathConstraint]]
 * [[SubPathConstraint]]
