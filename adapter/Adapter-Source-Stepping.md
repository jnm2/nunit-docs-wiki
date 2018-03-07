As of version 3.10, the NUnit3TestAdapter NuGet package and VSIX contain source-indexed PDBs for the adapter. Debuggers can step into the source code, set breakpoints, watch variables, etc. It’s easy to drop into NUnit adapter code any time you want to understand what’s going on.

If you’re getting ready to report a bug in the adapter, figuring out how to create a minimal repro is much easier since you aren’t dealing with a black box!

## How to step into adapter source in the Visual Studio debugger

The NUnit adapter PDBs are source-linked and work with Visual Studio 2017 or later.

 1. Turn **off** Debug > Options > ‘Enable Just My Code.’

    ℹ️ This is something you’ll want to leave on and only turn off when you want to step into source that isn’t contained in your solution.

    <img src="images/disable-just-my-code.png" width="50%" />

    (Next time you can make this faster by installing the excellent extension
    [Just My Code Toggle](https://marketplace.visualstudio.com/items?itemName=SamHarwell.JustMyCodeToggle).
    This allows you to set a keyboard shortcut along with adding a toolbar button and call stack context menu item.)

 2. If needed, turn **on** Debug > Options > ‘Enable Source Link support.’ This can usually be left on.

    <img src="images/enable-source-link-support.png" width="50%" />

 3. You can skip this section unless you are debugging a .NET Core assembly. Due to a packaging issue in 3.10, if you’re in the middle of debugging, you won't be able to step into adapter source until you copy `NUnit3.TestAdapter.pdb` to the output directory from `%userprofile%\.nuget\packages\nunit3testadapter\{version}\build\{target}` and continue debugging, or locate it manually when VS fails to find it. (If you’re using `packages.config`, it will be in the solution `packages` folder instead.)

    When your debugging session is finished, for a longer-term workaround that won’t have to be repeated on cleans or package upgrades, paste this into a [`Directory.Build.props`](https://docs.microsoft.com/en-us/visualstudio/msbuild/customize-your-build#directorybuildprops-example) or your own `Common.props` or into the .csprojs from which you are debugging:

    ```xml
      <!-- https://github.com/nunit/nunit3-vs-adapter/pull/480 -->
      <Target Name="IncludeAdapterSymbolsInOutput" BeforeTargets="BeforeBuild">
        <ItemGroup>
          <None Include="@(FileDefinitions->'%(ResolvedPath)')"
                Condition="'%(FileDefinitions.PackageName)' == 'NUnit3TestAdapter'
                       and '%(FileName)%(Extension)' == 'NUnit3.TestAdapter.pdb'"
                CopyToOutputDirectory="PreserveNewest" />
        </ItemGroup>
      </Target>
    ```

    And track the [thread](https://github.com/nunit/nunit3-vs-adapter/pull/480) linked in the comment to know when this workaround will no longer be needed.

 4. Congratulations! You can now use the debugger to step into method calls to the NUnit adapter and to set breakpoints and watch variables in the source! Keep in mind that it’s still a release build of the adapter, so variables and sequence points may not be available depending on runtime optimizations.
