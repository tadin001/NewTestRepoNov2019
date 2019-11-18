---
post_title: 'Test post 1 with text image gist code'
layout: post
post_status: future
post_date: 2019-11-18
userlogin:  qadevblogs
tags: dotnet, announcement
categories: visualstudio
featuredimage: https://github.com/tadin001/NewTestRepoNov2019/blob/master/FeaturedDefault.png
---
Test post to check if drafts from github get moved over to wordpress [DevBlogs][1].

# Important note ::
- this is H1 with single # 
- i committed directly into master

## What i tested in this post

This test post includes the following ... 

### types of content
- Text
- H2 header -- do H2s get links on them automatically? 
- H3 header
- Bullet list + numbered list
- Table
- Code
- Image -- github
- Gist -- github
- Iframe --  channel9
- Gif -- github
- Video files (mp4) -- github 
- CTA button shortcode 

### open Qs -- 
- how do i make TOC in markdown? 

### config settings in header
- post title
- author
- publish date in future
 - does this make it go live in future
 - or does it select that date keep post in draft state and not schedule a publish at this time?
- category
- tag
- featured image

## Title 1 within the post 
- this used 2 hashes
- does that translate to H2 properly? 

## Table 
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="623"><a href="http://devblogs.microsoft.com/cesardelatorre/wp-content/uploads/sites/32/2016/09/clip_image00224.png"><img style="padding-top: 0px; padding-left: 0px; padding-right: 0px; border-width: 0px;" title="clip_image002" src="https://devblogs.microsoft.com/wp-content/uploads/sites/32/2019/03/clip_image002_thumb14.png" alt="clip_image002" width="594" height="422" border="0" /></a></td>
<td valign="top" width="541"><span style="font-size: small;">In the Xamarin’s diagram you can see how you can share client code (usually C# app logic like ViewModels, Models, Service Agents, etc.) across the platforms between Xamarin.iOS, Xamarin.Android and even Windows 10 UWP projects. </span>

<span style="font-size: small;">If using Xamarin.Forms you can also share the same UI Code (Xamarin XAML defining the pages/views) between the platforms.</span>

&nbsp;</td>
</tr>
</tbody>
</table>

## Code
<pre><code class="cs">public void ConfigureServices(IServiceCollection services)
{
    ...
    services.AddSignalR()
            .AddAzureSignalR();
    ...
}

public void Configure(IApplicationBuilder app)
{
    ...
    app.UseAzureSignalR(routes =&gt; 
    { 
        routes.MapHub&lt;Chat&gt;("/chat"); 
    });
    ...
}
</code></pre>

## Image hosted in github
- Does this get moved over to WordPress?
- Or does it simply show in UI linking back to github as origin?

1. If linking back to github
2. that won't work given the repo is private (not public)
 ![useful image for this post](https://github.com/tadin001/NewTestRepoNov2019/blob/master/commit-graph-topo-order-git-1024x770.png)

## Gist
<script src="https://gist.github.com/bleroy/721a9375c62b352bde4e433fda45abeb.js"></script>

## Iframe
<iframe src="https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/New-XAML-Features-in-Visual-Studio/player" width="960" height="540" allowFullScreen frameBorder="0" title="New XAML Features in Visual Studio - Microsoft Channel 9 Video"></iframe>

## GIF
https://github.com/tadin001/NewTestRepoNov2019/blob/master/keybinding-blog-setbp.gif

## Video (mp4) files
https://github.com/tadin001/NewTestRepoNov2019/blob/master/IntelliCode-Video1.mp4

## CTA button
[cta-button text="Read More" url="https://devblogs.microsoft.com/visualstudio" color="#0078D4"]
[1]: https://devblogs.microsoft.com
