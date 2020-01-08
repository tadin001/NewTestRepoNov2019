---
ID: 222730
post_title: 'Testing Code Button &#8211; Span tag example'
author: qadevblogs
post_excerpt: ""
layout: post
permalink: >
  https://devblogs72.wpengine.com/visualstudio/testing-code-button-span-tag-example/
published: true
post_date: 2020-01-07 22:22:20
---
From MSDN when we migrated posts many came with tags that just wouldn't go away and required manual cleanup

here is one example from prod : https://devblogs.microsoft.com/premier-developer/demystifying-the-new-net-core-3-worker-service

Copied from Visual Editor into Visual editor >> 

Host.CreateDefaultBuilder(args) .ConfigureServices((hostContext, services) => { services.AddTransient<ICustomerService,CustomerService>(); services.AddHostedService<Worker>(); });

Copied from Visual Editor into Code button on Visual Editor >> without any manual formatting 

<pre class="prettyprint">Host.CreateDefaultBuilder(args) .ConfigureServices((hostContext, services) =&gt; { services.AddTransient&lt;ICustomerService,CustomerService&gt;(); services.AddHostedService(); });</pre>

Copied from Visual Editor into Code Button >> with line formatting

<pre class="prettyprint">Host.CreateDefaultBuilder(args) 
  .ConfigureServices((hostContext, services) =&gt; 
  { 
    services.AddTransient&lt;ICustomerService,CustomerService&gt;(); 
    services.AddHostedService(); 
  });</pre>

Copied from text editor into text editor >>

<pre class="lang:default decode:true"><span style="font-size: 10pt;">Host.CreateDefaultBuilder(args)
   .ConfigureServices((hostContext, services) =&gt;
   {
      services.AddTransient&lt;ICustomerService,CustomerService&gt;();
      services.AddHostedService&lt;Worker&gt;();
   });</span></pre>

Copied from text editor into code button on text editor >>

<pre class="lang:default decode:true"><span style="font-size: 10pt;">Host.CreateDefaultBuilder(args)
   .ConfigureServices((hostContext, services) =&gt;
   {
      services.AddTransient&lt;ICustomerService,CustomerService&gt;();
      services.AddHostedService&lt;Worker&gt;();
   });</span></pre>

 