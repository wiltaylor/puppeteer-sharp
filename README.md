# Puppeteer Sharp

[![NuGet](https://buildstats.info/nuget/PuppeteerSharp)][NugetUrl]
[![Build status](https://ci.appveyor.com/api/projects/status/pwfkjb0c4jfdo7lc/branch/master?svg=true&pendingText=master&failingText=master&passingText=master)][BuildUrl]
[![Demo build status](https://ci.appveyor.com/api/projects/status/10g64a4aa0083wgf/branch/master?svg=true&pendingText=demo&failingText=demo&passingText=demo)][BuildDemoUrl]
[![CodeFactor](https://www.codefactor.io/repository/github/kblok/puppeteer-sharp/badge)][CodeFactorUrl]

[NugetUrl]: https://www.nuget.org/packages/PuppeteerSharp/
[BuildUrl]: https://ci.appveyor.com/project/kblok/puppeteer-sharp/branch/master
[BuildDemoUrl]: https://ci.appveyor.com/project/kblok/puppeteer-sharp-0c8w9/branch/master
[CodeFactorUrl]: https://www.codefactor.io/repository/github/kblok/puppeteer-sharp

Puppeteer Sharp is a .NET port of the official [Node.JS Puppeteer API](https://github.com/GoogleChrome/puppeteer). 

# Useful links

* [API Documentation](http://www.puppeteersharp.com/api/index.html)
* Slack channel [#puppeteer-sharp](https://join.slack.com/t/puppeteer/shared_invite/enQtMzU4MjIyMDA5NTM4LTM1OTdkNDhlM2Y4ZGUzZDdjYjM5ZWZlZGFiZjc4MTkyYTVlYzIzYjU5NDIyNzgyMmFiNDFjN2UzNWU0N2ZhZDc)
* [StackOverflow](https://stackoverflow.com/search?q=puppeteer-sharp)
* [Issues](https://github.com/kblok/puppeteer-sharp/issues?utf8=%E2%9C%93&q=is%3Aissue)

# Prerequisites

 * As Puppeteer-Sharp is a NetStandard 2.0 library, The minimum platform versions are .NET Framework 4.6.1 and .NET Core 2.0. [Read more](https://docs.microsoft.com/en-us/dotnet/standard/net-standard).
 * The minimum Windows versions supporting the WebSocket library are Windows 8 and Windows Server 2012. [Read more](https://docs.microsoft.com/en-us/dotnet/api/system.net.websockets?redirectedfrom=MSDN&view=netframework-4.7.2).

# Usage

## Take screenshots

```cs
await new BrowserFetcher().DownloadAsync(BrowserFetcher.DefaultRevision);
var browser = await Puppeteer.LaunchAsync(new LaunchOptions
{
    Headless = true
});
var page = await browser.NewPageAsync();
await page.GoToAsync("http://www.google.com");
await page.ScreenshotAsync(outputFile);
```

You can also change the view port before generating the screenshot


```cs
await page.SetViewportAsync(new ViewPortOptions
{
    Width = 500,
    Height = 500
});
```


## Generate PDF files

```cs
await new BrowserFetcher().DownloadAsync(BrowserFetcher.DefaultRevision);
var browser = await Puppeteer.LaunchAsync(new LaunchOptions
{
    Headless = true
});
var page = await browser.NewPageAsync();
await page.GoToAsync("http://www.google.com");
await page.PdfAsync(outputFile);
```

## Inject HTML

```cs
using(var page = await browser.NewPageAsync())
{
    await page.SetContentAsync("<div>My Receipt</div>");
    var result = await page.GetContentAsync();
    await page.PdfAsync(outputFile);
    SaveHtmlToDB(result);
}
```

## Evaluate Javascript

```cs
using (var page = await browser.NewPageAsync())
{
    var seven = await page.EvaluateFunctionAsync<int>(“4 + 3”);
    var someObject = await page.EvaluateFunctionAsync<dynamic>("(value) => ({a: value})", 5);
    Console.WriteLine(someObject.a);
}
```

## Wait For Selector

```cs
using (var page = await browser.NewPageAsync())
{
    await page.GoToAsync("http://www.spapage.com");
    await page.WaitForSelectorAsync("div.main-content")
    await page.PdfAsync(outputFile));
}
```

## Wait For Function
```cs
using (var page = await browser.NewPageAsync())
{
    await page.GoToAsync("http://www.spapage.com");
    var watchDog = page.WaitForFunctionAsync("window.innerWidth < 100");
    await page.SetViewportAsync(new ViewPortOptions { Width = 50, Height = 50 });
    await watchDog;
}
```

## Connect to a remote browser

```cs
var options = new ConnectOptions()
{
    BrowserWSEndpoint = $"wss://www.externalbrowser.io?token={apikey}"
};

var url = "https://www.google.com/";

using (var browser = await PuppeteerSharp.Puppeteer.ConnectAsync(options))
{
    using (var page = await browser.NewPageAsync())
    {
        await page.GoToAsync(url);
        await page.PdfAsync("wot.pdf");
    }
}
```

# Monthly reports
 * [July 2018](https://www.hardkoded.com/blog/puppeteer-sharp-monthly-jul-2018)
 * [June 2018](http://www.hardkoded.com/blog/puppeteer-sharp-monthly-jun-2018)
 * [May 2018](http://www.hardkoded.com/blogs/puppeteer-sharp-monthly-may-2018)
 * [April 2018](http://www.hardkoded.com/blogs/puppeteer-sharp-monthly-april-2018)
 * [March 2018](http://www.hardkoded.com/blogs/puppeteer-sharp-monthly-march-2018)
 * [February 2018](http://www.hardkoded.com/blogs/puppeteer-sharp-monthly-february-2018)

# Progress

* Tests on Google's Puppeteer: 445.
* Tests on Puppeteer Sharp: 363.
* Passing tests: 362.
