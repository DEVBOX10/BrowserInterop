# BrowserInterop

[![Build Status](https://dev.azure.com/remibou/toss/_apis/build/status/RemiBou.BrowserInterop?branchName=master)](https://dev.azure.com/remibou/toss/_build/latest?definitionId=9&branchName=master) [![NuGet Badge](https://buildstats.info/nuget/BrowserInterop)](https://www.nuget.org/packages/BrowserInterop/)


This library provides access to browser API in a Blazor App. 

The following criteria are taken into account for choosing if an API must be handled :
- Is it already doable with Blazor (like XHR, DOM manipulation or already managed event ) ?
- Is that part of the standard ?
- Is that implemented by most browsers ? (> 75% in caniuse)

This library aim at providing some added value which are :
- Better deserialization than default : DomString, Infinity, Array-like map ...
- Better typing : duration as TimeSpan, string as enum ...
- Use IAsyncDisposable for method call that must be executed around a code block (like profiling) or event subscription
- Func for event subscription

I use the following website for discovering API description https://developer.mozilla.org/en-US/docs/Web/API and this one for finding out if it is implemented  https://caniuse.com/.

## Quick Start

First install the package 

```
dotnet add package BrowserInterop
```

Reference the needed JS in your index.html after the blazor.webassembly.js (or in your js bundling tool)

```html
    <script src="_framework/blazor.webassembly.js"></script>
    <script src="_content/BrowserInterop/scripts.js"></script>
```

Then in your template enter the API with the Window() extension method like this :

```c#
@using BrowserInterop.Extensions
...
@code {
    protected override async Task OnInitialized()
    {
        var window = await jsRuntime.Window();
        await window.Console.Log("this is a {0}","Log message");
      
    }
}
```

[==> More documentation and information on the wiki](https://github.com/RemiBou/BrowserInterop/wiki)

## Development

If you wish to improve this library here are a couple of things that might help you
### Environment

For working on this project you need the following tools installed on your machine :

- .NET SDK 3.1.202
- npm

### Projects

This repo is organised in 3 projects :
- src/BrowserInterop : the C# project for the netsstandard2.0 library
- sample/SampleApp : a sample app showing how to use BrowserInterop
- tests/BrowserInterop.E2ETests : the test suite, done with cypressio. All tests are located in cypress/integration folder.

### Run the test suite

- Run the app in sample/SampleApp :
```
dotnet watch run
```
- Open cypress Console in tests/BrowserInterop.E2ETests :
```
npm install
npm run-script start
```


