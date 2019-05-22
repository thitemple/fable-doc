---
title: Use a Fable library
---

[[toc]]

## Use a Fable library

We often use libraries using [NuGet](https://www.nuget.org/), which is the defacto .NET package manager.

So we do need libraries. And Fable proposes a great variety of libraries ready for you to use like:

- [Fable.Core](https://www.nuget.org/packages/Fable.Core/), which is required for every Fable project
- [Fable.Browser.Dom](https://www.nuget.org/packages/Fable.Browser.Dom), for all your DOM needs (window, document)
- [Fable.Elmish.React](https://www.nuget.org/packages/Fable.Elmish.React), to write web apps using the Elm architecture and React as the render engine
- [Thoth.Json](https://www.nuget.org/packages/Thoth.Json), for JSON serialization

> Please note that not all Nuget libraries will work with Fable. Refer to the library documentation to check if it's Fable-compatible.

There are 2 ways to call Fable libraries:

1 - Reference them directly in your project file
2 - Use [Paket](https://fsprojects.github.io/Paket/)

### Option 1: reference a library manually in your project file

Just like `.fs` files, we can reference libraries directly in the `.fsproj` file.

We need to tell what library we need and what version we'd like to use. For instance for `Fable.Browser.Dom` version `1.0.0` we'll add the following node in the `.fsproj` file:

```xml
<PackageReference Include="Fable.Browser.Dom" Version="1.0.0" />
```

Hence the standard format for a library:

```xml
<PackageReference Include="[PACKAGE_ID]" Version="[PACKAGE_VERSION]" />
```

The dotnet SDK offers a CLI command to do this operation without manually editing the .fsproj. Also if you omit the version number, it will automatically pick the most recent stable version for you. For instance:

`dotnet add package Fable.Elmish.React [-v 3.0.1]`

> Some IDEs like Visual Studio or Rider also include options in their Graphic Interface to manage Nuget packages.

That's basically all you need to do. The build process will then automatically download the libraries for you and compile your code against them.

> If you need to download the packages before the build (for example, to remove errors in the IDE), run the `dotnet restore` command in the folder containing the .fsproj file.

### Option 2: use Paket!

The second way of adding libraries is to use  the [Paket](https://fsprojects.github.io/Paket/) library manager. While it's not compulsory, it's in most cases a good choice for large projects.

Using Paket is clearly straightforward if you follow the [official documentation](https://fsprojects.github.io/Paket/getting-started.html)

But in order to make things easier for you, we created a [sample](https://github.com/fable-compiler/fable2-samples/tree/master/withpaket). This is a good companion while you read the paket doc.

Usually getting started with Paket takes only a few minutes.
