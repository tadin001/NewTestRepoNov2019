---
ID: 222667
post_title: 'PIX 1903.26 &#8211; Occupancy for Turing GPUs and Variable Rate Shading'
author: sivyel
post_excerpt: ""
layout: post
permalink: >
  https://devblogs72.wpengine.com/visualstudio/pix-1903-26-occupancy-for-turing-gpus-and-variable-rate-shading/
published: true
post_date: 2019-10-30 03:59:52
---
Today we released PIX-1903.26, available for download [here.][1] This release includes support for Variable Rate Shading in GPU Captures, and it adds support for Occupancy on NVIDIA Turing GPUs such as an RTX 2080.

[cta-button align="center" text="Read More" url="https://devblogs72.wpengine.com/visualstudio/" color="#0078D4"]

### Variable Rate Shading

Variable Rate Shading (VRS) is a powerful new DirectX 12 feature that allows applications to significantly reduce their pixel shading work in exchange for minimal loss of visual fidelity. It was announced last week over on the [DirectX blog][2].

PIX fully supports applications that use VRS. In particular, PIX's GPU Captures support capture and replay of VRS API calls. This allows VRS developers to inspect their shading rates in PIX and see the impact on their rendering work:

 

<img class="size-large wp-image-4285 aligncenter" src="http://devblogs.microsoft.com/pix/wp-content/uploads/sites/41/2019/03/pix_vrs-1024x619.png" alt="" width="640" height="387" />

 

*(Note: PIX had "Day One" support for VRS because the last PIX release secretly supported VRS! This is the first time we've discussed VRS on the PIX blog though.)*

 

### Occupancy on Turing

PIX's Occupancy graph is now supported on NVIDIA Turing GPUs (such as an RTX 2080) running driver 419.67 or later. This means that the Occupancy graph is now supported on all modern GPUs from NVIDIA and AMD. Many thanks to our IHV partners for making this possible!

The Occupancy graph complements PIX's other performance features such as High Frequency Counters, which are already supported on GPUs from AMD, Intel and NVIDIA. Here's an updated table of supported features on modern GPUs from each IHV:

 

<table class="aligncenter">
  <tbody>
    <tr>
      <td style="height: 27px;text-align: center;">
         
      </td>
      
      <td style="text-align: center;">
        <strong>Timing Analysis</strong>
      </td>
      
      <td style=" text-align: center;">
        <strong>Event List Counters</strong>
      </td>
      
      <td style=" text-align: center;">
        <strong>Occupancy</strong>
      </td>
      
      <td style=" text-align: center;">
        <strong>High Frequency Counters</strong>
      </td>
    </tr>
    
    <tr>
      <td style="width: 71px; height: 27px;">
        <strong>AMD</strong>
      </td>
      
      <td style="width: 96px; height: 27px; text-align: center;">
        ✓
      </td>
      
      <td style="width: 120px; height: 27px; text-align: center;">
        ✓
      </td>
      
      <td style="width: 91px; height: 27px; text-align: center;">
        ✓
      </td>
      
      <td style="width: 164px; height: 27px; text-align: center;">
        ✓
      </td>
    </tr>
    
    <tr>
      <td style="width: 71px; height: 27px;">
        <strong>Intel</strong>
      </td>
      
      <td style="width: 96px; height: 27px; text-align: center;">
        ✓
      </td>
      
      <td style="width: 120px; height: 27px; text-align: center;">
        ✓
      </td>
      
      <td style="width: 91px; height: 27px; text-align: center;">
        ✘
      </td>
      
      <td style="width: 164px; height: 27px; text-align: center;">
        ✓
      </td>
    </tr>
    
    <tr>
      <td style="width: 71px; height: 27px; text-align: left;">
        <strong>NVIDIA</strong>
      </td>
      
      <td style="width: 96px; height: 27px; text-align: center;">
        ✓
      </td>
      
      <td style="width: 120px; height: 27px; text-align: center;">
        ✓
      </td>
      
      <td style="width: 91px; height: 27px; text-align: center;">
        ✓
      </td>
      
      <td style="width: 164px; height: 27px; text-align: center;">
        ✓ (on Turing)
      </td>
    </tr>
  </tbody>
</table>

 

Please note that the Occupancy graph will be blank for DirectX Raytracing work. Insight into DirectX Raytracing workloads is possible via High Frequency Counters.

 

<img class="size-large wp-image-4303 aligncenter" src="http://devblogs.microsoft.com/pix/wp-content/uploads/sites/41/2019/03/turing_occupancy-1-910x1024.png" alt="" width="640" height="720" />

 

 

### High Frequency Counter Group Descriptions on NVIDIA

This release also adds a detailed description to each High Frequency Counter group on NVIDIA Turing GPUs. This will make it easier to navigate the list of counters.

<img class="size-full wp-image-4292 aligncenter" src="http://devblogs.microsoft.com/pix/wp-content/uploads/sites/41/2019/03/turing_hfc_descriptions.png" alt="" width="294" height="312" />

###  

 

### Other Changes

*   Miscellaneous fixes to the AMD plugin for High Frequency Counters
*   Based on user feedback, we've changed the High Frequency Counter icon to make it more discoverable

 

### Feedback

As always, if you have any feedback on PIX then please don't hesitate to use the feedback button (in the top-right corner of PIX) to contact us!

 [1]: http://devblogs.microsoft.com/pix/download/
 [2]: https://devblogs.microsoft.com/directx/variable-rate-shading-a-scalpel-in-a-world-of-sledgehammers/