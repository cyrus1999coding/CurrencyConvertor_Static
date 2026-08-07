# 001 WPF Currency Converter - Project overview and setup

We create the project using 🔑`WPF (.NET Framework)`

🧠 Remember ↓ 

## What is an Assembly ❓  

💡 GPT :  

An assembly is the compiled output of your C# project.

When you click Build, Visual Studio compiles your code into an assembly.

An assembly is usually either:

.exe → an executable application
.dll → a library

What's inside an assembly?

An assembly contains:

✅ Compiled IL (Intermediate Language) code
✅ Metadata (information about your code)
✅ Manifest (information about the assembly itself)
✅ Resources (images, icons, strings, etc., if included)

Assembly Metadata

This is what AssemblyInfo.cs (or the generated assembly information) is for.

Examples:
```cs
[assembly: AssemblyTitle("Airline API")]

[assembly: AssemblyVersion("1.0.0.0")]

[assembly: AssemblyCompany("Cyrus Software")]
```
This information becomes part of the assembly.

Why are assemblies useful?

Imagine you write a library:

```text
MathLibrary.dll
```

Another project can use it without needing the source code.

```text
Calculator.exe
        │
        ▼
MathLibrary.dll
```

Your application references the assembly and calls its methods.

EXE VS DLL ↓  

| EXE                  | DLL                    |
| -------------------- | ---------------------- |
| Can be run directly  | Cannot be run directly |
| Entry point (`Main`) | No entry point         |
| Application          | Library                |
| Both are assemblies  | Both are assemblies    |



1. WPF Application vs WPF (.NET Framework)

The main difference is which .NET platform they run on.

| WPF Application (.NET)                                       | WPF App (.NET Framework)              |
| ------------------------------------------------------------ | ------------------------------------- |
| Modern                                                       | Legacy                                |
| .NET 6 / 7 / 8 / 9 / 10                                      | .NET Framework 4.x                    |
| Cross-platform runtime (although WPF itself is Windows-only) | Windows-only runtime                  |
| Faster                                                       | Older                                 |
| Still actively developed                                     | Maintenance only                      |
| Recommended for new projects                                 | Only for maintaining old applications |

2. We need 🔑`Nuget package manger` (Individual Components)

NuGet is the package manager for .NET.

Think of it like:

| Language   | Package Manager |
| ---------- | --------------- |
| JavaScript | npm             |
| Python     | pip             |
| Java       | Maven           |
| .NET       | **NuGet**       |

It lets you install libraries written by Microsoft or other developers instead of writing everything yourself.

## Without NuGet

Imagine you need JSON support.

You'd have to write your own serializer.

That's thousands of lines of code.

## With NuGet

Install:

```terminal
Newtonsoft.Json
```

or

```terminal
Microsoft.EntityFrameworkCore
```

PostgreSQL support

```terminal
Npgsql.EntityFrameworkCore.PostgreSQL
```

Allows EF Core to work with PostgreSQL.


JWT

```terminal
Microsoft.AspNetCore.Authentication.JwtBearer
```

AutoMapper

```terminal
AutoMapper
```

Maps objects automatically.

FluentValidation

```terminal
FluentValidation
```

Validates models.

### Under the hood

When you install a package:

```terminal
Microsoft.EntityFrameworkCore
```

Visual Studio:

- downloads it
- stores it locally
- adds a reference to your project

Your .csproj file will contain something like:

```xml
<ItemGroup>
    <PackageReference Include="Microsoft.EntityFrameworkCore"
                      Version="9.0.0" />
</ItemGroup>
```



3. For the other parts we might want to install  
  - CLR data types for SQL Server
  - Data sources for SQL Server support 
  - SQL ADAL runtime
  - SQL Server Command Line Utilities
  - SQL Server Data Tools
  - SQL Server Express 2016 LocalDB
  - SQL Server ODBC Driver 

4. Optional (👀 Just for myself)
  ASP.NET and web development tools

`App.config` :  

```xaml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.2" />
    </startup>
</configuration>
```

- 🔑 This `App.config` is also written in `xaml` which can be changed per our requirenments so the  
  Adminstrator cna control which 🔑`protected resources` an application can Access which version of  
  🔑`Assembelies` will use .  
  The 🔑`connection string` for example for Databases which we're going to see later .

`App.xaml` :

```xaml
<Application x:Class="CurrencyConvertor_Static.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:local="clr-namespace:CurrencyConvertor_Static"
             StartupUri="MainWindow.xaml">
    <Application.Resources>
         
    </Application.Resources>
</Application>
```
- 🔑 Here we can add 🔑`Application Resources`, It's a place to  
  **Subscribe** to our Esssential 🔑`Application Events` like 🔑`Application Start` then 🔑`Unhandled Exceptions` and ...
- 🔑 It's the Declarative `starting point` of our application and the code behind is called `App.xaml.cs`

`App.xaml.cs`

```cs
using System;
using System.Collections.Generic;
using System.Configuration;
using System.Data;
using System.Linq;
using System.Threading.Tasks;
using System.Windows;

namespace CurrencyConvertor_Static
{
    /// <summary>
    /// Interaction logic for App.xaml
    /// </summary>
    public partial class App : Application
    {
    }
}
```
- This is the *Code behind File* which we can add the **Logic** to our project .