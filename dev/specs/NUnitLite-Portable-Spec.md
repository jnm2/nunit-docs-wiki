> **NOTE:** This page is a specification that was used as a starting point for creating the feature in NUnit. It needs to be reviewed and revised in order to accurately reflect what was actually built. If you take it with a grain of salt, it may still be helpful to you as documentation. This notice will be removed when the page is brought up to date.

### Supported Platforms ###

The portable framework will support the following platforms,

- .NET 4.5 on the desktop
- Silverlight 5
- Windows 8 Apps
- Windows Phone 8.1
- Windows Phone Silverlight 8
- Xamarin.Android
- Xamarin.iOS

For full support, we or third party providers will need to provide platform specific runners for each of the above platforms.

.NET 4.5 on the desktop is automatically supported since the functionality is minimal supported feature set. 

### NUnitLite Portable Assembly ###

The creation of the portable version of NUnitLite will allow NUnit to work on mobile devices like Android, Windows Phone, iOS, etc. It will also simplify maintaining NUnit on additional platforms since they can all be supported from one assembly. With the .NET framework being used on so many platforms, a portable version is the only maintainable approach to supporting these platforms.

Portable libraries are limited to the Framework APIs that are available on all of the targeted platforms. Because of this, they have limited thread, filesystem, serialization and appdomain support. Reflection is also limited, but not as badly. Because of this, NUnitLite Portable has the current Silverlight feature set minus the following;

- PlatformAttribute
- TimeoutAttribute
- DelayedConstraint
- Various threading attributes (MTA, STA)
- Various Path constraints
- All tests run on the main thread

Even though most of the Path constraints just work on strings, the base `PathConstraint` makes heavy use of `Path.DirectorySeparatorChar` and Path is not available in Portable. The only way we will know what the `DirectorySeparatorChar` is to rework the code will be to determine the OS, but the OS related classes aren't available either.

We may be able to get several of the deleted features working by reworking the reflection code and moving some code across the portable/runner boundary. 

For example, to re-introduce the PlatformAttribute, we could include it in the platform specific runners instead of in the framework assembly. It might also be possible to inject information from the runner into the framework at runtime.

### NUnitLite Runner ###

By definition, portable code cannot contain any runner code. The runner code needs to be in a platform specific assembly. To demonstrate how this works, I created an nunitlite.runner-sl-5.0 project and converted the Silverlight tests to use the portable library and the SilverLight framework.

We would then need to provide runners for each of the platforms we want NUnitLite to support, although we might want to leave some platforms up to others. For example, Xamarin already has decent NUnitLite 2.0 runners for iOS and Android.

### Future of NUnitLite ###

Depending on what we decide our vision is for the future of NUnitLite, the portable build might be rebranded NUnit for the various platforms it supports. The desktop version of NUnitLite is nearly feature compatible with the full framework. The CF version is adding features and becoming closer to the desktop version. Meanwhile, on phone platforms, we will be supporting a much smaller subset of features.

Either way, we will need to ship the portable framework and a runner per platform.