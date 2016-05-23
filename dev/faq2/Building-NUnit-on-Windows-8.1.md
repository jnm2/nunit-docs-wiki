## Update ##

We have updated the nunit.snk in version 3, so this does not apply. It does apply for NUnit 2.x, so if you are doing any work in the old repository, follow the instructions below, but note that the location of the nunit.snk files is different in that repository.

## Signing Error ##

There is a [bug in Windows 8.1](http://stackoverflow.com/questions/19861961/cryptoapi-sign-verify-not-working-on-windows-8-1-how-to-debug) that causes the build to fail with the following error,

    1>CSC : error CS1548: Cryptographic failure while signing assembly '...\nunit.framework.dll' -- 
    'Error signing assembly -- The parameter is incorrect. '

For now, if you are developing on Windows 8.1, you will need to create new **nunit.snk** files for your local development. To create **nunit.snk**, using the Visual Studio command prompt, run the following command at the root of the repository and then copy over any other copies in the repository.

`sn -k nunit.snk`

In the **nunit-framework** repository, it should be copied into the root directory and into _src\framework_.

In the **nunit-console** repository, it should be copied into the root directory, into _src\nunit.engine.api_ and into _src\nunit.engine_.

You need to ensure that you do not mistakenly check in this changed **nunit.snk** file into the repository. Git can ignore local changes to files by running the command,

`git update-index --assume-unchanged <files>`

If you ever need to undo the ignore, run the command

`git update-index --no-assume-unchanged <files>`

To make it easier, you can add these commands as aliases to your `.gitconfig` file.

    [alias]
      ignore = update-index --assume-unchanged
      unignore = update-index --no-assume-unchanged
