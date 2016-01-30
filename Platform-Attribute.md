The Platform attribute is used to specify platforms for which a test or fixture
should be run. Platforms are specified using case-insensitive string values
and may be either included or excluded from the run by use of the Include or 
Exclude properties respectively. Platforms to be included may alternatively
be specified as an argument to the PlatformAttribute constructor. In either
case, multiple comma-separated values may be specified.

If a test or fixture with the Platform attribute does not satisfy the specified
platform requirements it is skipped. The test does not affect the outcome of 
the run at all: it is not considered as ignored and is not even counted in 
the total number of tests. _[Ed.: Check this.]_ In the gui, the tree node for the test remains 
gray and the status bar color is not affected.

####Test Fixture Syntax

```C#
namespace NUnit.Tests
{
  using System;
  using NUnit.Framework;

  [TestFixture]
  [Platform("NET-2.0")]
  public class DotNetTwoTests
  {
    // ...
  }
}
```

####Test Syntax

```C#
namespace NUnit.Tests
{
  using System;
  using NUnit.Framework;

  [TestFixture]
  public class SuccessTests
  {
    [Test]
    [Platform(Exclude="Win98,WinME")]
    public void SomeTest()
    { /* ... */ }
}
```

####Platform Specifiers

The following values are recognized as platform specifiers.
They may be expressed in upper, lower or mixed case.

######Operating System

<ul>
<li>Win</li>
<li>Win32</li>
<li>Win32S</li>
<li>Win32Windows</li>
<li>Win32NT</li>
<li>WinCE</li>
<li>Win95</li>
<li>Win98</li>
<li>WinMe</li>
<li>NT3</li>
<li>NT4</li>
<li>NT5</li>
<li>NT6</li>
<li>Win2K</li>
<li>WinXP</li>
<li>Win2003Server</li>
<li>Vista</li>
<li>Win2008Server</li>
<li>Win2008ServerR2</li>
<li>Windows7</li>
<li>Win2012Server</li>
<li>Windows8</li>
<li>Unix</li>
<li>Linux</li>
<li>MacOsX</li>
<li>XBox</li>
</ul>

######Architecture

* 32-Bit
* 32-Bit-Process
* 32-Bit-OS (.NET 4.0 and higher only)
* 64-Bit
* 64-Bit-Process
* 64-Bit-OS (.NET 4.0 and higher only)

######Runtime

<ul>
<li>Net</li>
<li>Net-1.0</li>
<li>Net-1.1</li>
<li>Net-2.0</li>
<li>Net-3.0 (1)</li>
<li>Net-3.5 (2)</li>
<li>Net-4.0</li>
<li>Net-4.5 (3)</li>
<li>NetCF</li>
<li>SSCLI</li>
<li>Rotor</li>
<li>Mono</li>
<li>Mono-1.0</li>
<li>Mono-2.0</li>
<li>Mono-3.0 (4)</li>
<li>Mono-3.5 (5)</li>
<li>Mono-4.0</li>
</ul>

####Notes:

1. Includes Net-2.0
2. Includes Net-2.0 and Net-3.0
3. Includes Net-4.0
4. Includes Mono-2.0
5. Includes Mono-2.0 and Mono-3.0

