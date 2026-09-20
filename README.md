# Classic ASP.NET Web Application (.NET Framework) with Dependency Injection

> [!IMPORTANT]
> This repository has been retired and is no longer maintained. It is retained for historical
> reference and should not be treated as supported or secure production guidance.

This repository was born out of a need for web/application developers to migrate their somewhat out-dated ASP.NET MVC web application using the .NET Framework to the newest ASP.NET MVC Core release.

.NET Core as a fundamental rule uses dependency injection throughout, and ASP.NET Core is no exception to this rule, and yet a large number of traditional ASP.NET web applications do not use DI.

Given that developers and development teams are not usually given a lot of time to break apart an existing application just because they want to run on the latest all-singing and all-dancing framework, this repository serves as a simple example of how you can add DI to an existing 4.7.2 application.

Once you have added DI to your existing web application running under .NET Framework then a future migration to the .NET Core framework is much easier!

So this repository is a simple working example of how-to to get dependency injection and logging working in an older .NET Framework project using the [Microsoft.Extensions.DependencyInjection](https://www.nuget.org/packages/Microsoft.Extensions.DependencyInjection/) and [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/) packages.

Note: Both of these Extenions nuget packages are multi-targeted and so will work seamlessly when you finally get around upgrade to .NET Core.

This solution was built using Visual Studio and consists of;
- WebAppDI - ASP.NET Web Application (.NET Framework) utilising both MVC & Web API controllers
- WebAppDILib - .NET Framework class library.
- WebAppDI.Tests - .NET Framework class library for example unit tests.
- AzurePipelines - example [Azure Pipelines YAML build/test](https://docs.microsoft.com/en-us/azure/devops/pipelines/yaml-schema?view=azure-devops&tabs=schema) pipeline.

Before implementing the dependency injection, I performed some maintenance on the default project templates created by Visual Studio;
- I created a backup of all packages.config & web.config.
- Uninstalled all nuget packages from the Web Application project and manually deleted all binding redirects in the web.config file.
- Change Visual Studio to use nuget package reference ([see here](https://docs.microsoft.com/en-us/nuget/reference/migrate-packages-config-to-package-reference))
- Re-installed the nuget packages 1-by-1 into the Web Application until the project compiled (note client libraries like jquery & bootstrap should be re-installed using [libman](https://github.com/aspnet/LibraryManager/wiki/Using-LibMan-in-Visual-Studio) however I skipped that step for the example)
- Re-added some binding redirects into web.config which were explicitly required using values from the backup web.config taken in the first step!

The general steps I took to get DI working are as follows;
- Added nuget packages Microsoft.Owin & Microsoft.Owin.Host.SystemWeb
- Added a Startup.cs which contains the dependency resolvers for both MVC & Web API.
- Added example MVC and Web API Controllers to both the main Web Application and the class library.
- Created a test "service" to inject into both the Web API & MVC controllers called DITestService along with interface IDITestService.

The crucial code is in Startup.cs and in the Controller constructors which is where the dependency injection magic happens

I hope this repository helps you on your journey to upgrade to ASP.NET Core...

Hope this helps...

[![Build Status](https://dev.azure.com/f2calv/github/_apis/build/status/f2calv.WebAppDI?branchName=master)](https://dev.azure.com/f2calv/github/_build/latest?definitionId=1&branchName=master)