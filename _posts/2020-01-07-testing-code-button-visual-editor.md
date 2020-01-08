---
ID: 222727
post_title: 'Testing code button &#8211; Visual editor'
author: qadevblogs
post_excerpt: ""
layout: post
permalink: >
  https://devblogs72.wpengine.com/visualstudio/testing-code-button-visual-editor/
published: true
post_date: 2020-01-07 21:57:03
---
test post

<pre class="prettyprint">public class Customer
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

modelBuilder.Entity()
    .OwnsOne(c =&gt; c.Address);</pre>