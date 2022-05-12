# WinGetDotNet
Some easy-to-use [_WinGet_](https://docs.microsoft.com/en-us/windows/package-manager/winget) wrapper library for .NET

![wingetupd.exe](img/screenshot-source-code.png)

### What it is
It´s a simple and tiny .NET 6 library named WinGetDotNet, wrapping the popular Windows-App _WinGet_ (a tool by Microsoft, used to manage software packages on a Windows machine). WinGetDotNet makes it easy to integrate _WinGet_ into a .NET program.

WinGetDotNet is specifically designed with the [KISS principle](https://en.wikipedia.org/wiki/KISS_principle) in mind. It´s sole purpose is just to wrap _WinGet_ application process calls. Nothing else.

By the way: _WinGet_ is imo a __fantastic__ piece of software, to manage all of your Windows applications and keep your Windows software up2date. Fat kudos :thumbsup: to Microsoft here!  For more information about _WinGet_ itself, take a look at https://docs.microsoft.com/en-us/windows/package-manager/winget or use your Google-Fu techniques.

### How it works
- WinGetDotNet is released as .NET assembly (.dll). Just download and add it to your existing project.
- WinGetDotNet is released as .NET NuGet package (.nupkg). Just add it to your NuGet package source and use it.
- WinGetDotNet offers a method that asynchronously starts a _WinGet_ process as `Task`, to `await` the process.
- WinGetDotNet returns the _WinGet_ console output and exit code, after the awaitable process has finished.
- WinGetDotNet is using the `System.Diagnostics.Process` class to run _WinGet_.
- WinGetDotNet is using the TAP pattern, including typical `async/await` and `CancellationToken` concepts.
- WinGetDotNet is using a typical `CancellationToken` timeout pattern.
- WinGetDotNet is developed by using the [SOLID principles](https://en.wikipedia.org/wiki/SOLID) in a typical manner.

### Quick overview

Here are some excerpts, to give a quick overview on how it looks like, for a first impression:

- Property to verify if _WinGet_ is installed:
    ```csharp
    bool WinGetIsInstalled { get; }
    ```
- Method to run _WinGet_ asynchronous:
    ```csharp
    Task<WinGetResult> RunWinGetAsync(string parameters, CancellationToken cancellationToken = default)
    ```
- Method to run _WinGet_ asynchronous, with a given timeout:
    ```csharp
    Task<WinGetResult> RunWinGetAsync(string parameters, TimeSpan timeout, CancellationToken cancellationToken = default)
    ```
- Result model, containing data about how _WinGet_ was called, as well as it´s output and it´s exit code:
    ```csharp
    record WinGetResult(string ProcessCall, string ConsoleOutput, int ExitCode);
    ```
For more information, just use the IntelliSense tooltips of Visual Studio, or take a look into the source code. It´s really a rather small and simple library and not much more than what you see above. 😉

### Requirements
There aren´t any special requirements, besides having _WinGet_ installed on your machine. WinGetDotNet is just a typical .NET assembly, released as assembly DLL and NuGet package. Just download the newest release, from the [Releases](https://github.com/MBODM/WinGetDotNet/releases) page, unzip and add it to your project. All the releases are compiled for x64 Windows, assuming you are using some 64-bit Windows (and that's quite likely).

### Notes
- WinGetDotNet is under MIT license. Feel free to use the source and do whatever you want. I assume no liability.
- WinGetDotNet is written in C#, is using .NET 6 and is built with Visual Studio 2022.
- To compile the source by your own, you just need some Visual Studio 2022 edition. Nothing else.
- I never compiled it with other tools, like Rider or VS Code. I solely used Visual Studio 2022 Community.
- The release-binaries are compiled as _self-contained_ .NET 6 assemblies, with "_x64 Windows_" as target.
- _Self-contained_: That´s the reason why the binary-size may be bigger and why there is no framework dependency.
- GitHub´s default _.gitignore_ excludes Visual Studio 2022 publish-profiles, so i added a [screenshot](img/screenshot-publish-settings.png) to repo.
- WinGetDotNet offers a `Task` based approach, but the _WinGet_ app itself can´t run concurrently, without errors.
- So keep above fact in mind, before writing real concurrent code, by using i.e. `Task.WhenAll()` etc.
- WinGetDotNet just exists, because it started as a sidecar project of my  [wingetupd](https://github.com/MBODM/wingetupd) tool. :grin:

#### Have fun.

