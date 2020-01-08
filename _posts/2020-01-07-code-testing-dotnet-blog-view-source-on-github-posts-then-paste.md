---
ID: 222732
post_title: 'Code testing &#8211; DotNet blog &#8211; View Source on GitHub posts then paste'
author: qadevblogs
post_excerpt: ""
layout: post
permalink: >
  https://devblogs72.wpengine.com/visualstudio/code-testing-dotnet-blog-view-source-on-github-posts-then-paste/
published: true
post_date: 2020-01-07 22:45:37
---
# <a id="user-content-runtime-binding-behavior" class="anchor" aria-hidden="true" href="#runtime-binding-behavior"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Runtime Binding Behavior

<a href="https://docs.microsoft.com/dotnet/core/deploying/#framework-dependent-deployments-fdd" rel="nofollow">Framework-dependent</a> applications require a .NET Core host to find a compatible runtime from a central location. The behavior of runtime binding is critical for both application compatibility and runtime deployment convenience. <a href="https://docs.microsoft.com/dotnet/core/deploying/#self-contained-deployments-scd" rel="nofollow">Self-contained</a> apps don't have this need, because there is only one runtime they will ever use.

This document proposes a model that works for both apps and managed COM components/hosting.

Related content:

*   [Roll Forward On No Candidate Fx][1] doc defines existing behavior.
*   [Roll forward improvements for COM -- dotnet/core-setup #5062][2] specifies a proposal specific to COM.

## <a id="user-content-parts-of-a-version-number" class="anchor" aria-hidden="true" href="#parts-of-a-version-number"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Parts of a version number

.NET Core uses three-part version numbers, which include the following version components (in order):

*   major version
*   minor version
*   patch version

An example .NET Core version number is [2\.2.1][3].

Each of these version components is treated different for runtime binding, as discussed later in this document.

## <a id="user-content-specifing-a-net-core-runtime-version" class="anchor" aria-hidden="true" href="#specifing-a-net-core-runtime-version"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Specifing a .NET Core Runtime Version

Each application includes a .NET Core version dependency, specified as a three-part version. By default, this version is the `.0` patch for the two-part version specified by the target framework. We chose this model to allow applications to run on any machine that satisfies the target framework, and to instead make the specific version used a deployment choice.

You can see this model and the different files in which the various values are stored, in the following example.

<div class="highlight highlight-text-shell-session">
  <pre><span class="pl-c1">C:\testapps\twotwoapp&gt;dotnet new console</span>
<span class="pl-c1">C:\testapps\twotwoapp&gt;type twotwoapp.csproj</span>
<span class="pl-c1">&lt;Project Sdk="Microsoft.NET.Sdk"&gt;</span>

<span class="pl-c1">  &lt;PropertyGroup&gt;</span>
<span class="pl-c1">    &lt;OutputType&gt;Exe&lt;/OutputType&gt;</span>
<span class="pl-c1">    &lt;TargetFramework&gt;netcoreapp2.2&lt;/TargetFramework&gt;</span>
<span class="pl-c1">  &lt;/PropertyGroup&gt;</span>

<span class="pl-c1">&lt;/Project&gt;</span>
<span class="pl-c1">C:\testapps\twotwoapp&gt;dotnet build</span>
<span class="pl-c1">C:\testapps\twotwoapp&gt;type bin\Debug\netcoreapp2.2\twotwoapp.runtimeconfig.json</span>
<span class="pl-c1">{</span>
<span class="pl-c1">  "runtimeOptions": {</span>
<span class="pl-c1">    "tfm": "netcoreapp2.2",</span>
<span class="pl-c1">    "framework": {</span>
<span class="pl-c1">      "name": "Microsoft.NETCore.App",</span>
<span class="pl-c1">      "version": "2.2.0"</span>
<span class="pl-c1">    }</span>
<span class="pl-c1">  }</span>
<span class="pl-c1">}</span></pre>
</div>

The `version` property in `.runtimeconfig.json` file records the three-part version. As you can see, the `version` property specifies the `.0` patch for the `2.2` runtime, recorded as `2.2.0`.

You can specify a different version than `.0` patch. We only recommend specifying a different patch version if your application requires a specific patch version to run (due to a bug fix in the runtime), but this should be very uncommon. You can see a specific patch version being specified in the following example, with the `RuntimeFrameworkVersion` msbuild property set in the project file. This value is written to the `.runtimeconfig.json` file, similar to what was seen in the preceding example.

<div class="highlight highlight-text-shell-session">
  <pre><span class="pl-c1">C:\testapps\twotwoapp&gt;type twotwoapp.csproj</span>
<span class="pl-c1">&lt;Project Sdk="Microsoft.NET.Sdk"&gt;</span>

<span class="pl-c1">  &lt;PropertyGroup&gt;</span>
<span class="pl-c1">    &lt;OutputType&gt;Exe&lt;/OutputType&gt;</span>
<span class="pl-c1">    &lt;TargetFramework&gt;netcoreapp2.2&lt;/TargetFramework&gt;</span>
<span class="pl-c1">    &lt;RuntimeFrameworkVersion&gt;2.2.4&lt;/RuntimeFrameworkVersion&gt;</span>
<span class="pl-c1">  &lt;/PropertyGroup&gt;</span>

<span class="pl-c1">&lt;/Project&gt;</span>
<span class="pl-c1">C:\testapps\twotwoapp&gt;dotnet build</span>
<span class="pl-c1">C:\testapps\twotwoapp&gt;type bin\Debug\netcoreapp2.2\twotwoapp.runtimeconfig.json</span>
<span class="pl-c1">{</span>
<span class="pl-c1">  "runtimeOptions": {</span>
<span class="pl-c1">    "tfm": "netcoreapp2.2",</span>
<span class="pl-c1">    "framework": {</span>
<span class="pl-c1">      "name": "Microsoft.NETCore.App",</span>
<span class="pl-c1">      "version": "2.2.4"</span>
<span class="pl-c1">    }</span>
<span class="pl-c1">  }</span>
<span class="pl-c1">}</span></pre>
</div>

The .NET Core host attempts to find the best installed runtime given the three-part .NET Core version number specified in `.runtimeconfig.json`. If it cannot find a compatible runtime, it will print an error message similar to the following one.

<div class="highlight highlight-text-shell-session">
  <pre><span class="pl-c1">C:\testapps\twotwoapp&gt;dotnet bin\Debug\netcoreapp2.2\twotwoapp.dll</span>
<span class="pl-c1">It was not possible to find any compatible framework version</span>
<span class="pl-c1">The specified framework 'Microsoft.NETCore.App', version '2.2.4' was not found.</span>
<span class="pl-c1">  - Check application dependencies and target a framework version installed at:</span>
<span class="pl-c1">      C:\Program Files\dotnet\</span>
<span class="pl-c1">  - Installing .NET Core prerequisites might help resolve this problem:</span>
<span class="pl-c1">      http://go.microsoft.com/fwlink/?LinkID=798306&clcid=0x409</span>
<span class="pl-c1">  - The .NET Core framework and SDK can be installed from:</span>
<span class="pl-c1">      https://aka.ms/dotnet-download</span></pre>
</div>

The rest of the document discusses how to determine the *best installed runtime* for a given three-part version number.

## <a id="user-content-patch-version-selection" class="anchor" aria-hidden="true" href="#patch-version-selection"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Patch Version Selection

> This runtime selection logic is used to find an appropriate installed patch version for a given three-part runtime version (as specified in `.runtimeconfig.json`).

**Logic:** Given a request for `x.y.z` version, the host will look for all `x.y` versions that are equal or higher to `x.y.z`. It will select the highest patch version within that set. This behavior is oriented on selecting the most compatible and highest serviced (and therefore most secure) installed product version.

**User Impact:** When a user installs the latest patch version for the `x.y` version of .NET Core, all applications that target `x.y` will start using that newer patch version (on next application launch). The user does not need to configure their applications to use that latest serviced version.

Let's look at an example.

Requested version:

*   `2.2.0`

Installed versions:

*   `1.1.17`
*   `2.2.0`
*   `2.2.1`
*   `2.2.5`
*   `3.0.0`

In this scenario, the `2.2.5` runtime will be selected.

## <a id="user-content-minor-version-selection" class="anchor" aria-hidden="true" href="#minor-version-selection"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Minor Version Selection

> This runtime selection logic is used if an appropriate installed patch version for a given three-part runtime version (as specified in `.runtimeconfig.json`) cannot be found.

**Logic:** Given a request for `x.y.z` version, the host will look for an `x.y` runtime version, as described for **Patch Version Selection** above. If it cannot find an `x.y` runtime, then the host will look for all `x` runtimes that are higher than `x.y`. It will select the lowest minor version within that set and then select the highest patch version within that minor version.

If the host cannot find an `x` runtime, then the host shows an error message describing that the requested runtime could not be found. This behavior is oriented on selecting only a known compatible product version.

This behavior is oriented on selecting a known compatible installed product version.

**User Impact:** When a user runs an application on a machine that does not have `x.y` installed, but has a later minor version of `x`, then the app will transparently run on that later minor version.

Let's look at an example.

Requested version:

*   `2.1.0`

Installed versions:

*   `1.1.17`
*   `2.2.0`
*   `2.2.1`
*   `2.2.5`
*   `2.3.1`
*   `3.0.0`

In this scenario, the `2.2.5` runtime will be selected.

Let's look at another example.

Requested version:

*   `2.1.0`

Installed versions:

*   `1.1.17`
*   `3.0.0`

In this scenario, no runtime will be selected and instead the host prints a helpful error message (similar to the one displayed in the **Specifing a .NET Core Runtime Version** section).

We have found that this behavior is problematic for scenarios like <a href="https://twitter.com/KathleenDollard/status/1079811275641696256" rel="nofollow">global tools</a> and expect similar challenges for client applications (new with 3.0). To mitigate these scenarios, we will expose a set of configuration knobs to enable developers to opt-into a specific roll-forward behaviors for their app or their environment. We will write guidance for those scenarios to guide developers and end-users to opt-in to roll-forward for scenarios that will benefit from it. We will not provide templates that set these knobs automatically for developers.

## <a id="user-content-major-version-selection----opt-in-behavior-using-configuration-knobs" class="anchor" aria-hidden="true" href="#major-version-selection----opt-in-behavior-using-configuration-knobs"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Major Version Selection -- Opt-in Behavior using Configuration Knobs

> This runtime selection logic is used if an appropriate minor version for a given three-part runtime version cannot be found and an application or environment has been configured for major-version roll-forward via **Configuration Knobs** (defined in a following section).

Given a request for `x.y.z` version, the host will look for an `x` runtime version, as described for **Minor Version Selection** above. If it cannot find an `x` runtime, then the host will look for all runtimes that are higher than `x`. It will select the lowest major version within that set and then select the lowest minor and highest patch version within that set. This behavior is oriented on a best effort attempt at selecting a compatible installed product version. That's why the lowest minor version is selected, not the highest one.

**User Impact:** When a user runs an application on a machine that does not have `x` installed, but has a later runtime installed, then the app will transparently run on that later major version.

There is some risk in this scenario that the app will crash due to incompatibilities in the runtime relative to the runtime that the app targets and that it will be difficult to diagnose the cause (incompatibility) and the solution (installing a older runtime). If that app runs successfully, then the user will be happy. The tension between compatibility and deployment convenience is why this scenario is opt-in.

Let's look at an example.

Requested version:

*   `2.1.0`

Installed versions:

*   `1.1.17`
*   `3.0.0`
*   `3.0.1`
*   `3.1.0`
*   `4.0.0`

In this scenario, the `3.0.1` runtime will be selected.

## <a id="user-content-handling-previews" class="anchor" aria-hidden="true" href="#handling-previews"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Handling Previews

As of 3.0 Preview 2, previews have special binding behavior. In this proposal, previews are proposed to not have special behavior. Apps that depend on preview runtimes can bind to non-preview runtimes and vice-versa. Previews are not considered to be special going forward, with this proposal. This behavior is oriented on enabling applications built with previews to get a chance to run (likely successfully) on a stable version and to make testing stable applications on previews easy.

Assumption: Stable Visual Studio versions only install stable .NET Core versions.

## <a id="user-content-handling-frameworks" class="anchor" aria-hidden="true" href="#handling-frameworks"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Handling Frameworks

In .NET Core 3.0, components like ASP.NET Core, WPF and Windows Forms are modeled as *frameworks*. Frameworks follow the same binding rules as the runtime. The runtime is modeled as the lowest-level framework in the system.

The following example, the application depends on the `Microsoft.AspNetCore.App` framework, version `3.0.0-preview-19075-0444`. This framework is defined within the .NET Core installation and expresses a dependency on `Microsoft.NETCore.App`, version `3.0.0-preview-27324-5`. The host binds the frameworks according to these declarations.

<div class="highlight highlight-text-shell-session">
  <pre><span class="pl-c1">C:\testapps\threewebapp&gt;type threewebapp.csproj</span>
<span class="pl-c1">&lt;Project Sdk="Microsoft.NET.Sdk.Web"&gt;</span>

<span class="pl-c1">  &lt;PropertyGroup&gt;</span>
<span class="pl-c1">    &lt;TargetFramework&gt;netcoreapp3.0&lt;/TargetFramework&gt;</span>
<span class="pl-c1">  &lt;/PropertyGroup&gt;</span>


<span class="pl-c1">  &lt;ItemGroup&gt;</span>
<span class="pl-c1">    &lt;PackageReference Include="Microsoft.AspNetCore.Mvc.NewtonsoftJson" Version="3.0.0-preview-19075-0444" /&gt;</span>
<span class="pl-c1">  &lt;/ItemGroup&gt;</span>

<span class="pl-c1">&lt;/Project&gt;</span>

<span class="pl-c1">C:\testapps\threewebapp&gt;type bin\Debug\netcoreapp3.0\threewebapp.runtimeconfig.json</span>
<span class="pl-c1">{</span>
<span class="pl-c1">  "runtimeOptions": {</span>
<span class="pl-c1">    "tfm": "netcoreapp3.0",</span>
<span class="pl-c1">    "framework": {</span>
<span class="pl-c1">      "name": "Microsoft.AspNetCore.App",</span>
<span class="pl-c1">      "version": "3.0.0-preview-19075-0444"</span>
<span class="pl-c1">    },</span>
<span class="pl-c1">    "configProperties": {</span>
<span class="pl-c1">      "System.GC.Server": true</span>
<span class="pl-c1">    }</span>
<span class="pl-c1">  }</span>
<span class="pl-c1">}</span>
<span class="pl-c1">C:\testapps\threewebapp&gt;type C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App\3.0.0-preview-19075-0444\Microsoft.AspNetCore.App.runtimeconfig.json</span>
<span class="pl-c1">{</span>
<span class="pl-c1">  "runtimeOptions": {</span>
<span class="pl-c1">    "tfm": "netcoreapp3.0",</span>
<span class="pl-c1">    "framework": {</span>
<span class="pl-c1">      "name": "Microsoft.NETCore.App",</span>
<span class="pl-c1">      "version": "3.0.0-preview-27324-5"</span>
<span class="pl-c1">    }</span>
<span class="pl-c1">  }</span>
<span class="pl-c1">}</span></pre>
</div>

## <a id="user-content-com-components" class="anchor" aria-hidden="true" href="#com-components"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>COM Components

COM-based and other hosted environments have the requirement of loading managed components built for multiple runtime versions, and this set is typically not known a priori.

The application situation, described earlier in the doc, is largely oriented on missing runtime versions and how to handle that. The COM situation is oriented more on "best fit" for a set of components it may load. As a result, COM and other hosts need to artificially roll-forward to the latest acceptable runtime version to enable compatibility for arbitrary components.

We will offer a configuration knobs for hosts that enable artificial roll-forward. These knobs play a similar role to <a href="https://docs.microsoft.com/dotnet/framework/unmanaged-api/hosting/lockclrversion-function" rel="nofollow">LockClrVersion</a>.

## <a id="user-content-configuration-knobs" class="anchor" aria-hidden="true" href="#configuration-knobs"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Configuration Knobs

The host exposes the following configuration knobs that you can use to control binding behavior:

### <a id="user-content-version" class="anchor" aria-hidden="true" href="#version"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Version

The `version` knob specifies the minimum (or floor) version required by an application as a 3-part version.

`version` can be set in the following ways:

*   `RuntimeFrameworkVersion` in an MSBuild project
*   `version` in `.runtimeconfig.json`
*   `--fx-version` via the CLI

If `RuntimeFrameworkVersion` is not set, then `version` defaults to the `0` patch for the specified target framework. For example, `version` would be set to `3.0.0` by default for the `netcoreapp3.0` target framework.

MSBuild project settings are only consulted at build-time and are then written as properties to `.runtimeconfig.json`, which can be consulted at runtime.

### <a id="user-content-rollforward" class="anchor" aria-hidden="true" href="#rollforward"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>RollForward

`RollForward` specifies the roll-forward policy for an application, either as a fallback to accommodate missing a specific runtime version or as a directive to use a later version.

`RollForward` can have the following values:

*   `LatestPatch` -- Roll forward to the highest patch version. This disables minor version roll forward.
*   `Minor` -- Roll forward to the lowest higher minor version, if requested minor version is missing. If the requested minor version is present, then the `LatestPatch` policy is used.
*   `Major` -- Roll forward to lowest higher major version, and lowest minor version, if requested major version is missing. If the requested major version is present, then the `Minor` policy is used.
*   `LatestMinor` -- Roll forward to highest minor version, even if requested minor version is present.
*   `LatestMajor` -- Roll forward to highest major and highest minor version, even if requested major is present.
*   `Disable` -- Do not roll forward. Only bind to specified version. This policy is not recommended for general use since it disable the ability to roll-forward to the latest patches. It is only recommended for testing.

`Minor` is the default setting. See **Configuration Precedence** for more information.

In all cases except `Disable` the highest available patch version is selected.

Note: `LatestMinor` and `LatestMajor` are intended for component hosting scenarios, for both managed and native hosts (for example, managed COM components).

`RollForward` can be set in the following ways:

*   Project file property: `RollForward`
*   Runtime configuration file property: `rollForward`
*   Environment variable: `DOTNET_ROLL_FORWARD`
*   Command line argument: `--roll-forward`

### <a id="user-content-dotnet_roll_forward_on_no_candidate_fx" class="anchor" aria-hidden="true" href="#dotnet_roll_forward_on_no_candidate_fx"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>DOTNET_ROLL_FORWARD_ON_NO_CANDIDATE_FX

This setting is described in [Roll Forward On No Candidate Fx][1]. It does not have the right behavior or UX. We will deprecate this setting for 3.0.

The following policy will be used in 3.0:

*   If `ROLL_FORWARD_ON_NO_CANDIDATE_FX` is set, it will be honored.
*   If `ROLL_FORWARD` is set, it will be honored.
*   If both settings are set in the same scope, it is an error.
*   If neither settings are set, then the existing default behavior is used, as described in the **Patch Version Selection** and **Minor Version Selection** sections above. The default behavior is the same as setting `Minor`.

Note: The ENV syntax is used above, but the same rules apply for any way that the two settings are set.

### <a id="user-content-apply-patches" class="anchor" aria-hidden="true" href="#apply-patches"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Apply patches

This setting is described in [Roll Forward On No Candidate Fx][1]. Its interaction with the other settings is confusing. We will deprecate this setting for 3.0.

The following policy will be used in 3.0:

*   If `applyPatches` is set, it will be honored if the effective value of `RollForward` is one of `LatestPatch`, `Minor` and `Major`. In these cases setting `applyPatches` to `false` disables the automatic roll forward to latest patch version. If `RollForward` has any other value, the `applyPatches` is ignored.
*   If both settings are specified in the same scope, that is if `applyPatches` and `rollForward` are specified together in one `.runtimeconfig.json` file (anywhere in the file), it is an error.
*   If neither settings are set, then the existing default behavior is used, as described in the **Patch Version Selection** and **Minor Version Selection** sections above. The default behavior is the same as setting `Minor`.

Note: `applyPatches` can only be set in the runtime configuration file.

### <a id="user-content-configuration-precedence" class="anchor" aria-hidden="true" href="#configuration-precedence"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Configuration Precedence

The host will consult the various ways of setting `RollForward`, in order (later scopes take precedence over earlier ones):

1.  `.runtimeconfig.json` properties (AKA "json")
2.  Environment variables (AKA "ENV")
3.  CLI arguments

The `version` and `roll-forward` settings compose in the following way:

*   A `version` setting at higher precedent scopes overwrites both the `version` and `roll-forward` values at lower scopes. For example, `version` specified at the CLI scope (with `--fx-version`) overwrites both a `version` and `roll-forward` setting that might exist at the json scope.
*   A `version` setting can flow to higher scopes if it is not replaced by another `version` value. This enables a `roll-forward` setting at a higher scope to compose with a `version` setting at a lower scope.
*   The absence of a `version` value is an error.

More generally:

*   The `version` value establishes a floor for roll-forward behavior. The roll-forward process will never select a version lower than the effective value of the `version`.
*   The default `roll-forward` setting is `Minor` except when `--fx-version` is specified when it is `Disabled`.

## <a id="user-content-diagnostics" class="anchor" aria-hidden="true" href="#diagnostics"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Diagnostics

Runtime binding behavior and failures can be hard to diagnose. We will add events (maybe the same as runtime events, maybe different) that can be used to collect information about runtime binding behavior. This part of the plan needs to be better defined.

## <a id="user-content-runtime-binding-in-practice" class="anchor" aria-hidden="true" href="#runtime-binding-in-practice"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Runtime Binding in Practice

The following examples demonstrate various (non-exhaustive) ways that runtime binding behaves in practice, using `version` and `roll-forward` settings.

Installed versions:

*   `2.1.0`
*   `2.1.1`
*   `2.1.7`
*   `2.2.1`
*   `2.2.3`
*   `3.1.0`
*   `4.0.0`
*   `4.2.1`

<div class="highlight highlight-text-shell-session">
  <pre><span class="pl-c1">C:\testapps\twooneapp&gt;type twooneapp.csproj</span>
<span class="pl-c1">&lt;Project Sdk="Microsoft.NET.Sdk"&gt;</span>

<span class="pl-c1">  &lt;PropertyGroup&gt;</span>
<span class="pl-c1">    &lt;OutputType&gt;Exe&lt;/OutputType&gt;</span>
<span class="pl-c1">    &lt;TargetFramework&gt;netcoreapp2.1&lt;/TargetFramework&gt;</span>
<span class="pl-c1">  &lt;/PropertyGroup&gt;</span>

<span class="pl-c1">&lt;/Project&gt;</span>

<span class="pl-c1">C:\testapps\twooneapp&gt;type Program.cs</span>
<span class="pl-c1">using System;</span>

<span class="pl-c1">namespace twooneapp</span>
<span class="pl-c1">{</span>
<span class="pl-c1">    class Program</span>
<span class="pl-c1">    {</span>
<span class="pl-c1">        static void Main(string[] args)</span>
<span class="pl-c1">        {</span>
<span class="pl-c1">            Console.WriteLine("Hello World!");</span>
<span class="pl-c1">            Console.WriteLine(typeof(Object).Assembly.Location);</span>
<span class="pl-c1">        }</span>
<span class="pl-c1">    }</span>
<span class="pl-c1">}</span>

<span class="pl-c1">C:\testapps\twooneapp&gt;dotnet bin\Debug\netcoreapp2.1\twooneapp.dll</span>
<span class="pl-c1">Hello World!</span>
<span class="pl-c1">C:\Program Files\dotnet\shared\Microsoft.NETCore.App\2.1.7\System.Private.CoreLib.dll</span>

<span class="pl-c1">C:\testapps\twooneapp&gt;dotnet --fx-version 2.1.0 bin\Debug\netcoreapp2.1\twooneapp.dll</span>
<span class="pl-c1">Hello World!</span>
<span class="pl-c1">C:\Program Files\dotnet\shared\Microsoft.NETCore.App\2.1.0\System.Private.CoreLib.dll</span>

<span class="pl-c1">C:\testapps\twooneapp&gt;dotnet --fx-version 2.2.0 bin\Debug\netcoreapp2.1\twooneapp.dll</span>
<span class="pl-c1">It was not possible to find any compatible framework version</span>
<span class="pl-c1">The specified framework 'Microsoft.NETCore.App', version '2.2.0' was not found.</span>

<span class="pl-c1">C:\testapps\twooneapp&gt;dotnet --fx-version 2.2.0 --roll-forward Patch bin\Debug\netcoreapp2.1\twooneapp.dll</span>
<span class="pl-c1">Hello World!</span>
<span class="pl-c1">C:\Program Files\dotnet\shared\Microsoft.NETCore.App\2.2.3\System.Private.CoreLib.dll</span>

<span class="pl-c1">C:\testapps\twooneapp&gt;SET DOTNET_ROLL_FORWARD=LatestMajor</span>

<span class="pl-c1">C:\testapps\twooneapp&gt;dotnet bin\Debug\netcoreapp2.1\twooneapp.dll</span>
<span class="pl-c1">Hello World!</span>
<span class="pl-c1">C:\Program Files\dotnet\shared\Microsoft.NETCore.App\4.2.1\System.Private.CoreLib.dll</span>

<span class="pl-c1">C:\testapps\twooneapp&gt;dotnet --fx-version 2.2.0 bin\Debug\netcoreapp2.1\twooneapp.dll</span>
<span class="pl-c1">It was not possible to find any compatible framework version</span>
<span class="pl-c1">The specified framework 'Microsoft.NETCore.App', version '2.2.0' was not found.</span>

<span class="pl-c1">C:\testapps\twooneapp&gt;dotnet --fx-version 2.2.0 --roll-forward Patch bin\Debug\netcoreapp2.1\twooneapp.dll</span>
<span class="pl-c1">Hello World!</span>
<span class="pl-c1">C:\Program Files\dotnet\shared\Microsoft.NETCore.App\2.2.3\System.Private.CoreLib.dll</span></pre>
</div>

 [1]: https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md
 [2]: https://github.com/dotnet/core-setup/issues/5062
 [3]: https://github.com/dotnet/core/blob/master/release-notes/2.2/2.2.1/2.2.1.md