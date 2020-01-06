---
description: Settings for security behaviors
---

# Application Profiles

## Overview

The Application Profiles tab allows you to set appropriate security behaviors for your web applications. 

![Application Profiles View](../../../.gitbook/assets/image%20%2889%29.png)

Before configuring, ensure that the correct site is selected via the dropdown list at the upper right.

To add an entry to the list, click on the "+" button. To delete an entry, click on the "Remove" link next to its name.

{% hint style="info" %}
As shown in the above screenshot, the default \(“/”\)  profile will always be present. It applies to the entire site, except for those parts of the site that have specific profiles assigned to them.
{% endhint %}

Here are the fields for each Application Profile.

| Field Name | Description |
| :--- | :--- |
| **Label** | The name you have assigned to this particular entry. In the example screenshot, the labels are “Static Content” , “Default,” and “JS CSS". |
| **Pattern** | The list of extensions to which this profile will be applied, expressed as PCRE \(Perl Compatible Regular Expressions\). An explanation and some examples are here: [Pattern Matching Syntax](../../../reference-information-1/pattern-samples.md).  |
| **Protect** | When enabled, this tells Reblaze to inspect all requests for the specified destination. This should always be enabled, unless there is a specific reason not to do so.  |
| **WebSocket** | Enables support for the WebSocket protocol for this resource. |
| **Cache Mode** | Defines Reblaze’s cache behavior for the resources specified in this profile. Modes are explained here: [Controlling Caching Behavior](../../../using-the-product/how-do-i.../cache-modes.md).  |
| **Client TTL**  | Custom expiration time for the Client Side cache, in [TTL Expression Syntax](../../../reference-information-1/custom-ttl-values.md). \(Entries will show as strikethroughs when the Cache Mode is set to an option where the TTL values are ignored.\) |
| **CDN TTL** | Custom expiration time for the CDN Side cache, in [TTL Expression Syntax](../../../reference-information-1/custom-ttl-values.md). \(Entries will show as strikethroughs when the Cache Mode is set to an option where the TTL values are ignored.\) |
| **Purge  Content** | Purges the cache and removes its content. See explanation below. |

## Purge Cache

If you'd like to clear cache on one of your websites on the platform, you can click the "Purge" button. Usually, the action takes around 5 minutes. 

{% embed url="https://youtu.be/4ZpJTpTrKQc" %}

