NUnit uses a standard naming convention for all tests - however, this can be overridden by the user if required. TestName generation is driven by a name formatting string, which may contain any of the following format specifiers:

  * `{n}` The namespace of the test or empty if there is no namespace. If empty, any immediately following '.' is ignored.

  * `{c}` The class name of the test or empty if there is no class. This name includes any type arguments, enclosed in angle braces and separated by commas.

  * `{C}` The full name of the class. Equivalent to `{n}.{c}`

  * `{m}` The method name of the test or empty if there is no method. The name includes any type arguments, enclosed in angle braces and separated by commas.

  * `{M}` The full name of the method. Equivalent to `{n}.{c}.{m}` or `{C}.{m}`

  * `{a}` The full argument representation, enclosed in parentheses and separated by commas. Each argument is represented by the standard NUnit format for certain types, otherwise by the result of ToString().

  * `{0}`, `{1}`...`{9}`. An individual argument. This form is only useful when setting the name of an individual test case. If used in the default format string, any arguments not used will be ignored.

  * `{i}` The test id, which is normally of the form mmm-nnn.

  * Any text not included between curly braces is copied to the name as is.

After the name is formatted, any leading or trailing '.' characters are removed. Otherwise, all non-format characters in the string are included as is.

String arguments may be truncated to a maximum length. Either the {a} specifier or any of the individual argument specifiers may be followed by a colon and a length:

  * `{a:40}` Truncate __each string argument__ to 40 characters. All strings more than 37 characters are truncated to the first 37 followed by "..."

  * `{0:20}` Truncate argument zero to 20 characters.

#### Standard Name Formats		
		
Internally, NUnit uses certain standard formats unless overridden by the user. The standard format for generating a name from a test method and its arguments is:

```
         {m}{a:40} // Name
         {M}{a:40} // FullName
```

This leads to test names like:

```
         Test1
         Test2(5, 2)
         Test3("This is the argument")
         Test4("This is quite long argument, so it is...")
```

#### Modifying the Name Format

The SetName property of TestCaseData allow setting the format string for the individual test case. So long as no format specifiers are used in the name, there will be no change in how this works. Any format specifier will trigger regeneration of the test name according to what is provided. For example, if the user wishes to specify only the argument portion of the name of a test method, while retaining the method name, the name could be set to

```
         {m}(User argument)
```

This would result in the display of the test name as

```
         SomeMethod(User Argument)
```

Note that in this usage, it will generally only make sense to use `{m}`, `{a}` or `{0}` through `{9}` specifiers. However, NUnit will use whatever is provided.
