---
post_title: 'Test post 3 - nov 17 - 3'
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
1. first 2 tests both showed up in wordpress as drafts - so that is good
2. they both took a few mins to show 
- refresh didn't work 
- is there any way to force a pull from WP / or is it best to just wait for a few mins? 

VS blog was set to default visual = html editor
so I am testing again after changing the editor to markdown   

# What worked in test 1 and 2
- publish date was correct -- state was still drafts -- that is good
- all header info taken in well - author, category, tag
- numbered list
- bullet list
- CTA button

# What didn't work and I am testing a third time to check 
- featured image
- H2 did not get links -- is this just not enabled in Dev72 ? If not - why ?? 
- image -- did not work! shows the broken image icons
- gist -- missing entirely
- iframe -- missing  entirely
- gif -- i'm not sure how to insert so i have put it in circular braces for now similar to images / png
- video -- got this rror msg - Media error: Format(s) not supported or source(s) not found. I am not sure how to address this and if it just a matter of me doing something differnet to make this work. This might need soem more investigation. 

# What maybe worked... i am testing with some adjustment
- table -- it had an image and used the table html tags. So I added a new tabke with more columns and rows copied over from a markdown wordpress view in dotnet blog - 
https://devblogs.microsoft.com/dotnet/wp-admin/post.php?post=24904&action=edit
- code also seeemed to work so-so trying again now with crayon disabled and prettify enabled 

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
| Product Version                                               | Cumulative Update                                                                                                                                                                        |
| ------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Windows 10 1809 (October 2018 Update) Windows Server 2019** | **<a href="http://www.catalog.update.microsoft.com/Search.aspx?q=4520405" rel="nofollow">Catalog</a>** **<a href="https://support.microsoft.com/kb/4520405" rel="nofollow">4520405</a>** |
| .NET Framework 3.5, 4.7.2                                     | <a href="http://www.catalog.update.microsoft.com/Search.aspx?q=4519569" rel="nofollow">Catalog</a> <a href="https://support.microsoft.com/kb/4519569" rel="nofollow">4519569</a>         |
| .NET Framework 3.5, 4.8                                       | <a href="http://www.catalog.update.microsoft.com/Search.aspx?q=4519565" rel="nofollow">Catalog</a> <a href="https://support.microsoft.com/kb/4519565" rel="nofollow">4519565</a>         |
| **Windows 10 1803 (April 2018 Update)**                       |                                                                                                                                                                                          |
| .NET Framework 3.5, 4.7.2                                     | <a href="http://www.catalog.update.microsoft.com/Search.aspx?q=4519978" rel="nofollow">Catalog</a> <a href="https://support.microsoft.com/kb/4519978" rel="nofollow">4519978</a>         |
| .NET Framework 4.8                                            | <a href="http://www.catalog.update.microsoft.com/Search.aspx?q=4519572" rel="nofollow">Catalog</a> <a href="https://support.microsoft.com/kb/4519572" rel="nofollow">4519572</a>         |
| **Windows 10 1709 (Fall Creators Update)**                    |                                                                                                                                                                                          |
| .NET Framework 3.5, 4.7.1, 4.7.2                              | <a href="http://www.catalog.update.microsoft.com/Search.aspx?q=4520006" rel="nofollow">Catalog</a> <a href="https://support.microsoft.com/kb/4520006" rel="nofollow">4520006</a>         |
| .NET Framework 4.8                                            | <a href="http://www.catalog.update.microsoft.com/Search.aspx?q=4519564" rel="nofollow">Catalog</a> <a href="https://support.microsoft.com/kb/4519564" rel="nofollow">4519564</a>         |
| **Windows 10 1607 (Anniversary Update) Windows Server 2016**  |                                                                                                                                                                                          |
| .NET Framework 3.5, 4.6.2, 4.7, 4.7.1, 4.7.2                  | <a href="http://www.catalog.update.microsoft.com/Search.aspx?q=4519979" rel="nofollow">Catalog</a> <a href="https://support.microsoft.com/kb/4519979" rel="nofollow">4519979</a>         |
| .NET Framework 4.8                                            | <a href="http://www.catalog.update.microsoft.com/Search.aspx?q=4519562" rel="nofollow">Catalog</a> <a href="https://support.microsoft.com/kb/4519562" rel="nofollow">4519562</a>         |

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
![Gif test](https://github.com/tadin001/NewTestRepoNov2019/blob/master/keybinding-blog-setbp.gif)

(https://github.com/tadin001/NewTestRepoNov2019/blob/master/keybinding-blog-setbp.gif)

## Video (mp4) files
https://github.com/tadin001/NewTestRepoNov2019/blob/master/IntelliCode-Video1.mp4

## CTA button
[cta-button text="Read More" url="https://devblogs.microsoft.com/visualstudio" color="#0078D4"]
[1]: https://devblogs.microsoft.com
