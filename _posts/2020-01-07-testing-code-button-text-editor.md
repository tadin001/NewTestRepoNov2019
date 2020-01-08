---
ID: 222726
post_title: 'Testing Code Button &#8211; Text editor'
author: qadevblogs
post_excerpt: ""
layout: post
permalink: >
  https://devblogs72.wpengine.com/visualstudio/testing-code-button-text-editor/
published: true
post_date: 2020-01-07 21:54:40
---
Testing code button <pre class="prettyprint">public class Customer
{
    public int Id { get; set; }
    public string Name {get; set;}
    public PhysicalAddress Address { get; set; }
}

public class PhysicalAddress
{
    public string StreetAddress { get; set; }
    public Location Location { get; set; }
}

...

modelBuilder.Entity&lt;customer>()
    .OwnsOne(c => c.Address);&lt;/customer></pre>