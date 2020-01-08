---
ID: 222733
post_title: 'Code test &#8211; copied from markdown &#8211; with prettify enabled via writing settings'
author: qadevblogs
post_excerpt: ""
layout: post
permalink: >
  https://devblogs72.wpengine.com/visualstudio/code-test-copied-from-markdown-with-prettify-enabled-via-writing-settings/
published: true
post_date: 2020-01-07 22:52:57
---
# ASP.NET Core updates in .NET Core 3.0 Preview 2

[.NET Core 3.0 Preview 2 is now available][1] and it includes a bunch of new updates to ASP.NET Core.

Here's the list of what's new in this preview: - Razor Components - SignalR client-to-server streaming - Pipes on HttpContext - Generic host in templates - Endpoint routing updates

## Get started

To get started with ASP.NET Core in .NET Core 3.0 Preview 2 [install the .NET Core 3.0 Preview 2 SDK][2]

If you're on Windows using Visual Studio, you'll also want to [install the latest preview of Visual Studio 2019][3].

## Upgrade an existing project

To upgrade an existing an ASP.NET Core app to .NET Core 3.0 Preview 2, follow the [migrations steps in the ASP.NET Core docs][4].

### Add package for Json.NET

example of script

<script src="https://gist.github.com/richlander/7213b5dcaf011ad0cbe3d2582697b228.js"></script> example of iframe

<iframe width="560" height="315" allowfullscreen="allowfullscreen" frameborder="0" src="https://www.youtube.com/embed/hLFyycJVo0I"></iframe> 
As part of the work to [tidy up the ASP.NET Core shared framework][5], Json.NET is being removed from the shared framework and now needs to be added as a package.

To add back Json.NET support to an ASP.NET Core 3.0 project: - Add a package reference to [Microsoft.AspNetCore.Mvc.NewtonsoftJson][6] - Update your `ConfigureServices` method to include a call to `AddNewtonsoftJson()`.

<pre><code class="csharp">services.AddMvc()
    .AddNewtonsoftJson();
</code></pre>

### Working with Razor Components

Razor Components are self-contained chunks of user interface (UI), such as a page, dialog, or form. Razor Components are normal .NET classes that define UI rendering logic and client-side event handlers, so you can write rich interactive web apps without having to write any JavaScript. Razor components are typically authored using Razor syntax, a natural blend of HTML and C#. Razor Components are similar to Razor Pages and MVC Views in that they both use Razor. But unlike pages and views, which are built around a request/reply model, components are used specifically for handling UI composition.

To create, build, and run your first ASP.NET Core app with Razor Components run the following from the command line:

    dotnet new razorcomponents -o WebApplication1
    cd WebApplication1
    dotnet run
    

Here's what the `Counter` component code looks like:

<pre><code class="html">@page "/counter"

&lt;h1&gt;Counter&lt;/h1&gt;

&lt;p&gt;Current count: @currentCount&lt;/p&gt;

&lt;button class="btn btn-primary" onclick="@IncrementCount"&gt;Click me&lt;/button&gt;

@functions {
    int currentCount = 0;

    void IncrementCount()
    {
        currentCount+=1;
    }
}
</code></pre>

Making a request to `/counter`, as specified by the `@page` directive at the top, causes the component to render its content. Components render into an in-memory representation of the render tree that can then be used to update the UI in a very flexible and efficient way. Each time the "Click me" button is clicked the `onclick` event is fired and the `IncrementCount` method is called. The `currentCount` gets incremented and the component is rendered again. The runtime compares the newly rendered content with what was rendered previously and only the changes are then applied to the DOM (i.e. the updated count).

You can use components from other components using an HTML-like syntax where component parameters are specified using attributes or child content. For example, you can add a `Counter` component to the app's home page like this:

<pre><code class="html">@page "/"

&lt;h1&gt;Hello, world!&lt;/h1&gt;

Welcome to your new app.

&lt;Counter /&gt;
</code></pre>

To add a parameter to the `Counter` component update the `@functions` block to add a property decorated with the `[Parameter]` attribute:

<pre><code class="csharp">@functions {
    int currentCount = 0;

    [Parameter] int IncrementAmount { get; set; } = 1;

    void IncrementCount()
    {
        currentCount+=IncrementAmount;
    }
}
</code></pre>

Now you can specify `IncrementAmount` parameter value using an attribute like this:

<pre><code class="html">&lt;Counter IncrementAmount="10" /&gt;
</code></pre>

This is just an intro to what Razor Components are capable of. Razor Components are based on the Blazor component model and they support all of the same features (parameters, child content, templates, lifecycle events, component references, etc.). To learn more about Razor Components check out the [component model docs][7] and [try out building your first Razor Components app][8] yourself.

### Hosting Razor Components

<pre><code class="html">@inject IJSRuntime JS

&lt;button onclick="@OnClick"&gt;Show prompt&lt;/button&gt;

@functions {
    string name;

    async Task OnClick() {
        name = await JS.Prompt("Hi! What's you're name?");
    }
}
</code></pre>

Both Razor Components and Blazor share the same JavaScript interop abstraction, so .NET libraries relying on JavaScript interop are usable by both types of apps. Check out the [JavaScript interop docs][9] for more details on using JavaScript interop and the [Blazor community page][10] for existing JavaScript interop libraries.

### Sharing component libraries

Components can be easily shared and reused just like you would normal .NET classes. Razor Components can be built into component libraries and then shared as NuGet packages. You can find existing component libraries on the [Blazor community page][10].

The JavaScript code would then use the `subject.next` method to handle strings as they are captured and ready to be sent to the server.

<pre><code class="javascript">subject.next("example");
subject.complete();
</code></pre>

Using code like the two snippets above, you can create real-time streaming experiences. For a preview of what you can do with client-side streaming with SignalR, take a look at the demo site, [streamr.azurewebsites.net][11]. If you create your own stream, you can stream ASCII art representations of image data being captured by your local web cam to the server, where it will be bounced out to other clients who are watching your stream.

 [1]: https://blogs.msdn.microsoft.com/dotnet/2019/01/29/announcing-net-core-3-preview-2/
 [2]: https://dotnet.microsoft.com/download/dotnet-core/3.0
 [3]: https://visualstudio.com/preview
 [4]: https://docs.microsoft.com/en-us/aspnet/core/migration/22-to-30
 [5]: https://blogs.msdn.microsoft.com/webdev/2018/10/29/a-first-look-at-changes-coming-in-asp-net-core-3-0/
 [6]: https://nuget.org/packages/Microsoft.AspNetCore.Mvc.NewtonsoftJson
 [7]: https://blazor.net/docs/components/index.html
 [8]: https://blazor.net/docs/tutorials/build-your-first-blazor-app.html
 [9]: https://blazor.net/docs/javascript-interop.html
 [10]: https://blazor.net/community
 [11]: http://streamr.azurewebsites.net